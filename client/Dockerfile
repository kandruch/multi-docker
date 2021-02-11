# Use an existing docker image as a base
FROM node:alpine as builder

# Download and install dependencies
WORKDIR /usr/app
COPY ./package.json /usr/app
RUN npm install
COPY ./ ./
RUN npm run build

FROM nginx
EXPOSE 3000
# Tell the image what to do when it starts as a container
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=0 /usr/app/build /usr/share/nginx/html