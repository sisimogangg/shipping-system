FROM golang:1.9.0 as builder 

WORKDIR /go/src/github.com/sisimogangg/shippy/consignment-cli

COPY . . 

RUN go mod download

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .


FROM debian:latest

RUN apk --no-cache add ca-certificates

RUN mkdir -p /app
WORKDIR /app
COPY consignment.json /app/consignment.json

COPY --from=builder /go/src/github.com/sisimogangg/shippy/consignment-cli/consignment-cli .

CMD ["./consignment-cli"]
