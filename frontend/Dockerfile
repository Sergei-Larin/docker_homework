# ---- Base Node ----
FROM alpine:3.15 AS base
# install node
RUN apk add --no-cache nodejs npm
# set working directory
WORKDIR /frontend
# copy project file
COPY package.json .
#
# ---- Dependencies ----
FROM base AS dependencies
# set build arg
ARG HOST_IP
# install node packages
RUN npm install --loglevel verbose
# copy source app
COPY . .
# change host ip address
RUN for i in $(grep -ir localhost:8000 . | cut -f1 -d ":"); do sed -i "s/localhost/$HOST_IP/" $i;done
# build project
RUN npm run build --verbose
#
# ---- Release ----
FROM nginx:alpine
# set working directory
WORKDIR /frontend 
# copy build files
COPY --from=dependencies /frontend/build/ .
# expose port
EXPOSE 80
