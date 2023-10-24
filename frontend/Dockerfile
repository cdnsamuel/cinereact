# Dockerfile frontend
# build environment
FROM node:16.14 as builder

RUN mkdir /usr/src/app
WORKDIR /usr/src/app

ENV PATH /usr/src/app/node_modules/.bin:$PATH

ARG VITE_TMDB_API_KEY=${VITE_TMDB_API_KEY}
ENV VITE_TMDB_API_KEY=${VITE_TMDB_API_KEY}
ARG VITE_TMDB_URL=${VITE_TMDB_URL}
ENV VITE_TMDB_URL=${VITE_TMDB_URL}
ARG VITE_TMDB_URL_IMAGE=${VITE_TMDB_URL_IMAGE}
ENV VITE_TMDB_URL_IMAGE=${VITE_TMDB_URL_IMAGE}

COPY ./frontend /usr/src/app

RUN npm install -g npm@10.2.0
RUN npm install
RUN npm run build

# production environment
FROM nginx:1.15
COPY --from=builder /usr/src/app/dist /usr/share/nginx/html
COPY ./frontend/default.conf /etc/nginx/conf.d/
EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]