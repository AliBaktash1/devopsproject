FROM golang:1.20-alpine AS build


RUN mkdir -p app/sender


WORKDIR /app/sender


ENV GOPATH /go
ENV GOCACHE /go-build
ENV GO111MODULE=on
ENV GOOS=linux
ENV CGO_ENABLED=0

COPY go.mod ./
COPY go.sum ./
RUN  go mod download

COPY . .

RUN go build -o result ./

FROM alpine:3.18.2

RUN mkdir project

WORKDIR /project

COPY --from=build /app/sender/result .

EXPOSE 9090

CMD [ "./result" ]