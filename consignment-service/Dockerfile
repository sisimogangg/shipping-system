FROM golang:alpine as builder

RUN apk --no-cache add git

WORKDIR /app/consignment-service

COPY . . 

RUN go mod download

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o consignment-service

FROM debian:latest

# Security related package, good to have.
RUN apk --no-cache add ca-certificates

RUN mkdir /app
WORKDIR /app

COPY --from=builder /app/consignment-service/consignment-service .

CMD ["./consignment-service"]