FROM node:20 AS build
ARG BRANCH=master
ARG DOMAIN_URL=https://jeecg.56982.com:8888/jeecg-boot
ENV NODE_OPTIONS=--max-old-space-size=4096
RUN npm i -g pnpm@8.15.9
WORKDIR /src
RUN git clone --depth 1 --branch ${BRANCH} https://github.com/jeecgboot/jeecgboot-vue3.git .
RUN sed -i "s#^VITE_GLOB_DOMAIN_URL=.*#VITE_GLOB_DOMAIN_URL=${DOMAIN_URL}#" .env.production && grep VITE_GLOB .env.production
RUN pnpm install
RUN pnpm build

FROM nginx:alpine
COPY --from=build /src/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
