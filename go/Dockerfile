# First stage: Build the Go binary
FROM golang:1.20 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module and sum files to the container
COPY go.mod go.sum ./

# Download the Go dependencies
RUN go mod download

# Copy the rest of the application code into the container
COPY . .

# Build the Go application binary (statically linked, CGO_ENABLED=0)
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o myapp .

# Second stage: Create a minimal image to run the application
FROM alpine:latest

# Install CA certificates (necessary for HTTPS requests)
RUN apk --no-cache add ca-certificates

# Copy the Go binary from the builder image
COPY --from=builder /app/myapp /usr/local/bin/myapp

# Expose port 8080 for the Go application
EXPOSE 8080

# Run the Go application
CMD ["/usr/local/bin/myapp"]
