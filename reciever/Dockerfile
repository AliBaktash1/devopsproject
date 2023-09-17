FROM golang:1.20-alpine AS build


RUN mkdir -p app/reciever


WORKDIR /app/reciever


ENV GOPATH /go
ENV GOCACHE /go-build
ENV GO111MODULE=on
ENV GOOS=linux
ENV CGO_ENABLED=0

COPY go.mod ./
COPY go.sum ./


COPY . .


RUN  go mod download
RUN go build -o result ./

FROM alpine:3.18.2

RUN mkdir project

WORKDIR /project

COPY --from=build /app/reciever/result .

# EXPOSE 9292

CMD [ "./result" ]

