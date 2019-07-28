FROM golang:1.12.7 as builder

WORKDIR /go/src/github.com/sisimogangg/shippy/vessel-service

COPY . .

RUN go get -u github.com/golang/dep/cmd/dep
RUN dep init && dep ensure
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .


FROM debian:latest

RUN apk --no-cache add ca-certificates

RUN mkdir /app
WORKDIR /app
COPY --from=builder /go/src/github.com/sisimogangg/shippy/vessel-service/vessel-service .

CMD ["./vessel-service"]