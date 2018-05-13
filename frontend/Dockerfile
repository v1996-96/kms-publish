FROM alpine/git AS git
WORKDIR /app
RUN git clone git://github.com/v1996-96/kms-frontend.git .

FROM node:latest
ARG API_HOSTNAME
ENV API_HOSTNAME ${API_HOSTNAME}
WORKDIR /app
COPY --from=git /app .
RUN npm install --no-optional
RUN npm run build
EXPOSE 8080
ENTRYPOINT ["node", "./build/server.js"]
