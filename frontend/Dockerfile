FROM node:20 AS build
ARG BRANCH=master
ENV NODE_OPTIONS=--max-old-space-size=4096
RUN npm i -g pnpm@8.15.9
WORKDIR /src
RUN git clone --depth 1 --branch ${BRANCH} https://github.com/jeecgboot/jeecgboot-vue3.git .
RUN pnpm install
RUN pnpm build

FROM nginx:alpine
COPY --from=build /src/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
