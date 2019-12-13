FROM golang:1.13-alpine as golang-base
FROM alpine as alpine-base

FROM golang-base as build
RUN apk add alpine-sdk

RUN mkdir /app
WORKDIR /app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

RUN go build -o /go/bin/app

FROM alpine-base
RUN apk add --no-cache ca-certificates curl \
    && adduser -S me
COPY --from=build /go/bin/app /usr/local/bin/app

USER me

CMD ["app"]
EXPOSE 8080
