# Use a minimal base image with Go installed
FROM golang:1.13 as builder

# Set working directory
WORKDIR /go/src/app

# Copy the source code (assuming it’s available locally)
COPY . .

# Build the Go application
RUN go build -o guestbook

# Use a minimal runtime image
FROM alpine:3.10

# Install CA certificates
RUN apk --no-cache add ca-certificates

# Set working directory
WORKDIR /app

# Copy the compiled Go binary from the builder stage
COPY --from=builder /go/src/app/guestbook .

# Expose the application port
EXPOSE 80

# Start the application
CMD ["./guestbook"]
