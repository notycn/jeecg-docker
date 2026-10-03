FROM node:20 AS build

ARG BRANCH=v3.9.5
ARG DOMAIN_URL=https://jeecg.56982.com:8888/jeecg-boot

ENV NODE_OPTIONS=--max-old-space-size=8192

RUN npm i -g pnpm@9

WORKDIR /src

RUN git clone --depth 1 --branch ${BRANCH} https://github.com/jeecgboot/JeecgBoot.git .

WORKDIR /src/jeecgboot-vue3

RUN sed -i "s#^VITE_GLOB_DOMAIN_URL=.*#VITE_GLOB_DOMAIN_URL=${DOMAIN_URL}#" .env.production \
    && grep VITE_GLOB .env.production

RUN pnpm install --frozen-lockfile
RUN pnpm build

FROM nginx:alpine

COPY --from=build /src/jeecgboot-vue3/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
