FROM golang:1.22-alpine

ENV GO111MODULE=on
RUN apk add --no-cache git
ADD . /go/src/gitlab.com/opsplane-services/alloy-remote-config-server
WORKDIR /go/src/gitlab.com/opsplane-services/alloy-remote-config-server
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /alloy-remote-config-server cmd/config/main.go

FROM alpine:3.16.0
RUN apk add --no-cache ca-certificates
COPY --from=0 /alloy-remote-config-server /
EXPOSE 8888 8080
CMD ["/alloy-remote-config-server"]
