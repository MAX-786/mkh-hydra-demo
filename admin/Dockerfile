
# syntax=docker/dockerfile:1
FROM plone/plone-frontend:latest AS ploneadmin

ENV RAZZLE_API_PATH="https://mkh-hydra-demo-api.fly.dev"
ENV RAZZLE_PUBLIC_URL="https://mkh-hydra-demo-admin.fly.dev"
# ENV RAZZLE_INTERNAL_API_PATH="http://backend-volto.fly.dev/Plone"
# ENV RAZZLE_INTERNAL_API_PATH="http://backend-volto.internal:8080/Plone"  # Doesn't start the machine. needs flycast
# ENV RAZZLE_DEV_PROXY_API_PATH="http://backend-volto.fly.dev/Plone/++api++"
# ENV RAZZLE_PROXY_REWRITE_TARGET="/VirtualHostBase/https/hydra.pretagov.com/++api++/VirtualHostRoot"
ENV DEBUG_HPM=1


EXPOSE 3000
#CMD [ "pnpm", "start:prod" ]

