# Build stage: Compile the Go app
FROM golang:1.16 AS builder

WORKDIR /app

# Copy go.mod and go.sum first for dependency caching
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the source code
COPY . .

# Build the Go binary
RUN go build

# Expose the port
EXPOSE 8080

# Set environment variables
ENV PORT=8080
ENV REQUEST_ORIGIN=http://localhost:3000/

# Run the server
CMD ["./server"]

# start with `docker build -t example-backend .` and `docker run -p 8080:8080 example-backend`
