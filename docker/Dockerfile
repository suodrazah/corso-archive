# syntax=docker/dockerfile:1

# This dockerfile is able to make a quick, local image of corso.
# It is not used for deployments.

## Build
FROM golang:1.22 AS base

WORKDIR /src

COPY ./src/go.mod .
COPY ./src/go.sum .
RUN go mod download

COPY ./src .

FROM base AS build
ARG TARGETOS
ARG TARGETARCH
RUN GOOS=${TARGETOS} GOARCH=${TARGETARCH} go build -o /corso .

## Deploy
FROM ubuntu:22.10

COPY --from=build /corso /

USER nobody

ENTRYPOINT ["/corso"]
