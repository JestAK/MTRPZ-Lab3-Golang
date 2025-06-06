FROM golang:1.19-buster 

WORKDIR /app

COPY ../../go.mod ../../go.sum .
RUN go mod download

COPY ../../main.go .
COPY ../../cmd ./cmd
COPY ../../lib ./lib
COPY ../../templates ./templates 

RUN CGOOS=linux CGO_ENABLED=0 go build -o app .

EXPOSE 8080

ENTRYPOINT ["./app"]