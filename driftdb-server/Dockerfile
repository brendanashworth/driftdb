FROM rust:1.72-slim

WORKDIR /usr/src/driftdb

# Copy the entire project to build the server
COPY . .

# Build the server with release profile
WORKDIR /usr/src/driftdb/driftdb-server
RUN cargo build --release

# Install necessary runtime dependencies
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*

# Move the built binary to the path
RUN cp /usr/src/driftdb/target/release/driftdb-server /usr/local/bin/driftdb-server

# Expose the port the server runs on
EXPOSE 8080

# Run the server
CMD ["driftdb-server", "--host", "0.0.0.0"]