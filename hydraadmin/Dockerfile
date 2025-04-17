
FROM node:20-slim AS base
ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
COPY ./volto-hydra/ /app
RUN npm install -g corepack
RUN corepack cache clean
RUN corepack enable
WORKDIR /app

FROM base AS prod-deps
WORKDIR /app
RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm install --prod --frozen-lockfile

FROM base AS build
WORKDIR /app

RUN apt-get -y update && apt-get -y install git make
RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm dlx mrs-developer missdev --no-config --fetch-https \
    && pnpm install --frozen-lockfile
RUN pnpm run build
RUN ls -al /app

FROM base
COPY --from=prod-deps /app/node_modules /app/node_modules
COPY --from=build /app/core/packages/volto/build /app/core/packages/volto/build
COPY --from=build /app/core/packages/volto/package.json /app/core/packages/volto/package.json
COPY --from=build /app/core/packages/volto/node_modules /app/core/packages/volto/node_modules
COPY --from=build /app/core/packages /app/core/packages

ENV RAZZLE_DEFAULT_IFRAME_URL="https://mkh-hydra-demo-frontend.netlify.app"  
ENV RAZZLE_API_PATH="https://mkh-hydra-demo-api.fly.dev"
ENV RAZZLE_PUBLIC_URL="https://mkh-demo.fly.dev"
# ENV RAZZLE_INTERNAL_API_PATH="http://backend-volto.fly.dev/Plone"
# ENV RAZZLE_INTERNAL_API_PATH="http://backend-volto.internal:8080/Plone"  # Doesn't start the machine. needs flycast
# ENV RAZZLE_DEV_PROXY_API_PATH="http://backend-volto.fly.dev/Plone/++api++"
# ENV RAZZLE_PROXY_REWRITE_TARGET="/VirtualHostBase/https/hydra.pretagov.com/++api++/VirtualHostRoot"
ENV DEBUG_HPM=1


EXPOSE 3000
CMD [ "pnpm", "start:prod" ]



# http.get('http://backend-volto.fly.dev/Plone', (resp) => {
#   let data = '';

#   // A chunk of data has been received.
#   resp.on('data', (chunk) => {
#     data += chunk;
#   });
#   // The whole response has been received. Print out the result.
#   resp.on('end', () => {
#     console.log(JSON.parse(data).explanation);
#   });

# }).on("error", (err) => {
#   console.log("Error: " + err.message);
# });