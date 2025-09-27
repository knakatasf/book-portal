# ---- Build React ----
FROM node:20-alpine AS build
WORKDIR /app
ENV CI=true
COPY package.json package-lock.json* ./
RUN npm ci --no-audit --no-fund
COPY . .
RUN CI= npm run build

# ---- Serve with Nginx ----
FROM nginx:1.27-alpine
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx/nginx.conf /etc/nginx/conf.d/app.conf
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 3000
CMD ["nginx","-g","daemon off;"]

## build environment
#FROM node:alpine as build
#WORKDIR /app
#ENV PATH /app/node_modules/.bin:$PATH
#COPY package.json /app/package.json
#RUN npm install --silent
#COPY . /app
#RUN npm run build
#
## production environment
#FROM nginx:alpine
#COPY --from=build /app/build /usr/share/nginx/html
#RUN rm /etc/nginx/conf.d/default.conf
#COPY ./nginx/nginx.conf /etc/nginx/conf.d
#EXPOSE 3000
#CMD ["nginx", "-g", "daemon off;"]
