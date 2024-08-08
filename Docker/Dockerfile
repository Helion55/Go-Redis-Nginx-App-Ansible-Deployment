FROM golang:1.21
EXPOSE 8080

ENV DEMO_APP_ADDR=127.0.0.1:8080 
ENV DEMO_REDIS_ADDR= redis:6379

WORKDIR /usr/src/app

COPY go.mod .
COPY go.sum .
COPY main.go .

RUN go build -o bin .
ENTRYPOINT ["/usr/src/app/bin"]
