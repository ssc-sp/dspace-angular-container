FROM node:14-alpine AS build
WORKDIR /app

ADD  ./ /app/

RUN yarn install && \
    yarn build:prod && \
    yarn cache clean

FROM node:14-alpine AS run
WORKDIR /dspace-ui

COPY  --chown=node:node --from=build /app/dist /dspace-ui/dist
COPY  --chown=node:node --from=build /app/config/config.example.yml /dspace-ui/config/config.prod.yml

USER node

EXPOSE 4000
CMD [ "node", "./dist/server/main.js" ]