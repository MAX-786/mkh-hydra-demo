# syntax=docker/dockerfile:1
ARG PLONE_VERSION=6.1
FROM plone/plone-backend:${PLONE_VERSION} AS plonebackend


ARG SEED=1000
ENV CORS_ALLOW_ORIGIN="*"
ENV CORS_ALLOW_METHODS="DELETE,GET,OPTIONS,PATCH,POST,PUT"
ENV CORS_ALLOW_CREDENTIALS="true"
ENV CORS_EXPOSE_HEADERS="Content-Length"

ENV SITE="Plone"
# ENV RELSTORAGE_DSN="dbname='plone' user='plone' host='pg-demo-db.flycast' password='...'"
    
# TODO: this needs to be added manually. and api doesn't seem to work without removing /Plone
ENV VHM_MAPPING="mkh-hydra-demo-api.fly.dev/VirtualHostBase/https/mkh-hydra-demo-api.fly.dev/Plone/VirtualHostRoot/"
# ENV DELETE_EXISTING="True"
ENV SITE_ID="Plone"


# listen on ipv6 and ip4. needed for fly.io internal connection
RUN sed -i 's/0.0.0.0/*/g' etc/zope.ini

ENTRYPOINT [ "/app/docker-entrypoint.sh" ]
CMD ["start"]
