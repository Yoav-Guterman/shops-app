# packaging a dev env:

# FROM node:22-alpine

# WORKDIR /app

# COPY ./package*.json ./

# RUN npm install

# COPY ./ ./

# CMD npm run dev


# packaging a from production:

FROM node:22-alpine as builder
WORKDIR /app 
COPY ./package*.json ./
RUN npm install
COPY ./ ./
RUN npm run build -- --configuration docker
# RUN npm run build


FROM nginx:alpine
WORKDIR /usr/share/nginx/html
RUN rm -rf *
COPY --from=builder /app/dist/02-social-network-client ./
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
ENTRYPOINT [ "nginx", "-g", "daemon off;" ]

# # Build stage
# FROM node:22-alpine as builder
# WORKDIR /app
# COPY ./package*.json ./
# RUN npm install
# COPY ./ ./
# RUN npm run build

# # Production stage
# FROM nginx:alpine
# WORKDIR /usr/share/nginx/html
# RUN rm -rf *
# COPY --from=builder /app/dist/nature-websites-client ./
# COPY ./nginx.conf /etc/nginx/conf.d/default.conf
# ENTRYPOINT ["nginx", "-g", "daemon off;"]