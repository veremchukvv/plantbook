FROM golang:1.16.4-alpine3.13 as builder
WORKDIR /app
COPY go.* ./
RUN go mod download
COPY . ./

ARG BUILD_NUMBER
ARG GITSHA

RUN echo $BUILD_NUMBER
RUN echo $GITSHA

ENV BUILD_NUMBER1=$BUILD_NUMBER
ENV GITSHA1=$GITSHA

RUN echo $BUILD_NUMBER1
RUN echo $GITSHA1
RUN apk update && apk add date
RUN GOOS=linux GOARCH=amd64 CGO_ENABLED=0 \
    go build -a -tags netgo -ldflags "-s -w -extldflags '-static' -X 'github.com/veremchukvv/plantbook/internal/api/restapi.build=$BUILD_NUMBER1' -X 'github.com/veremchukvv/plantbook/internal/api/restapi.buildAt=$(date -Iseconds)' -X 'github.com/veremchukvv/plantbook/internal/api/restapi.githash=$GITSHA1'" \
    -o plantbook-server ./cmd/plantbook-server

FROM scratch as app
ENV PORT=8081
ENV METRICPORT=8082
ENV HOST=0.0.0.0
WORKDIR /app
COPY --from=builder /app/plantbook-server /app/plantbook-server
ENTRYPOINT ["./plantbook-server"]
CMD ["--scheme=http"]
LABEL org.opencontainers.image.source https://github.com/veremchukvv/plantbook
EXPOSE $PORT $METRICPORT