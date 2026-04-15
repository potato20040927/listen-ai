FROM golang:1.23-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o main .

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/main .
RUN mkdir -p /data
ENV SQLITE_PATH=/data/listenai.db
ENV STAT_PORT=8002
EXPOSE 8002
CMD ["./main"]