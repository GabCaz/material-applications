# Build stage: Compile the Go app
FROM golang:1.16 AS builder

# Set workdir for build stage
WORKDIR /app

# Copy go.mod and go.sum first for dependency caching
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the source code
COPY . .

# Build the Go binary (stays as root for now, since build often needs root permissions)
RUN go build -o server

# Create a non-root user and group
RUN useradd -m appuser

# Change ownership of /app directory to the new user
RUN chown -R appuser:appuser /app

# Switch to non-root user
USER appuser

# Expose the port
EXPOSE 8080

# Set environment variables
ENV PORT=8080
ENV REQUEST_ORIGIN=http://localhost

# Run the server as non-root
CMD ["./server"]

# Build and run:
# docker build -t example-backend .
# docker run -p 8080:8080 example-backend