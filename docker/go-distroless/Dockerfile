FROM golang:1.19-buster AS builder

WORKDIR /app

COPY ../../go.mod ../../go.sum .
RUN go mod download

COPY ../../main.go .
COPY ../../cmd ./cmd
COPY ../../lib ./lib
COPY ../../templates ./templates 

RUN CGOOS=linux CGO_ENABLED=0 go build -o app .

FROM gcr.io/distroless/base-debian12

COPY --from=builder /app/templates  ./templates
COPY --from=builder /app/app /app

EXPOSE 8080

ENTRYPOINT ["./app", "serve"]