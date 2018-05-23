FROM golang:latest

ARG BINARY_PATH

WORKDIR /app
COPY ${BINARY_PATH} /app/

# Run benchmark tool when the container starts
ENTRYPOINT ["./inch"]