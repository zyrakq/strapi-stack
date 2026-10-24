# Creating multi-stage build for production
FROM node:22-alpine AS build
RUN apk update && apk add --no-cache build-base gcc autoconf automake zlib-dev libpng-dev vips-dev git > /dev/null 2>&1
ARG NODE_ENV=production
ARG STRAPI_VERSION=latest

ENV NODE_ENV=${NODE_ENV}
ENV STRAPI_TELEMETRY_DISABLED=true
ENV CI=true
WORKDIR /opt/app

RUN yes n | npx create-strapi@${STRAPI_VERSION} temp --skip-cloud --skip-db --no-example --no-git-init --no-run --install --typescript && \
    cp -a temp/. . && \
    rm -rf temp
RUN yarn config set network-timeout 600000 -g
RUN yarn build

# Creating final production image
FROM node:22-alpine
RUN apk add --no-cache vips-dev
ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}
WORKDIR /opt/app
COPY --from=build /opt/app ./
ENV PATH=/opt/node_modules/.bin:$PATH

RUN chown -R node:node /opt/app
USER node
EXPOSE 1337
CMD ["yarn", "develop"]