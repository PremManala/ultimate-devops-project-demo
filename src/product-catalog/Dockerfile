FROM golang:latest AS builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download


RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o product-catalog .

FROM alpine AS release 

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/product-catalog ./
COPY ./products ./products

RUN chmod +x product-catalog

ENV PRODUCT_CATALOG_PORT=8088
ENTRYPOINT ["./product-catalog"]

