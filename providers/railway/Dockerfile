# syntax = docker/dockerfile:1.6
FROM ghcr.io/joshstevens19/rrelayer:latest AS rrelayer

ARG PROJECT_PATH="./example-project"

WORKDIR /usr/src/app

COPY ${PROJECT_PATH} /usr/src/app/rrelayer-app

ARG PORT="3000"
ENV PORT=${PORT}

EXPOSE ${PORT}

ENTRYPOINT ["/app/rrelayer"]
CMD ["start", "-p", "./rrelayer-app"]
