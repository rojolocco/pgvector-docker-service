# Pgvector Docker Service

A ready-to-use Docker service for running [pgvector](https://github.com/pgvector/pgvector), a PostgreSQL extension for vector similarity search. This service makes it easy to deploy and manage a pgvector instance for your vector database needs.

## What is pgvector?

pgvector is an open-source PostgreSQL extension that adds support for vector similarity search. It allows you to:

- Store embeddings as a native data type
- Find similar vectors using exact and approximate nearest neighbor search
- Use multiple indexing methods (IVFFlat, HNSW)
- Perform vector operations directly in SQL

This makes it ideal for applications involving:

- Machine learning
- Natural language processing
- Image similarity search
- Recommendation systems
- Semantic search

## Features of this Docker Service

- Pre-configured pgvector container based on PostgreSQL 16
- Persistent data storage
- Health checks for reliability
- Resource limits for predictable performance
- Network integration with Caddy for easy proxying
- Environment-based configuration

## Requirements

- Docker and Docker Compose
- At least 512MB RAM and 0.5 CPU cores available for the container

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/pgvector-docker-service.git
   cd pgvector-docker-service
   ```

2. Create a `.env` file based on the example:

   ```bash
   cp .env.example .env
   ```

3. Edit the `.env` file to set your PostgreSQL credentials:

   ```env
   POSTGRES_USER=postgres
   POSTGRES_PASSWORD=your_secure_password
   POSTGRES_DB=postgres
   ```

4. Start the service:

   ```bash
   docker-compose up -d
   ```

## Configuration

The service can be configured through environment variables in the `.env` file:

| Variable | Description | Default |
|----------|-------------|---------|
| POSTGRES_USER | PostgreSQL username | postgres |
| POSTGRES_PASSWORD | PostgreSQL password | (empty) |
| POSTGRES_DB | PostgreSQL database name | postgres |

Additional configuration can be done by modifying the `docker-compose.yaml` file.

## Usage

### Connecting to the Database

You can connect to the pgvector database using any PostgreSQL client:

```bash
psql -h localhost -p 5432 -U postgres -d postgres
```

### Creating a Vector Column

```sql
-- Enable the pgvector extension
CREATE EXTENSION IF NOT EXISTS vector;

-- Create a table with a vector column
CREATE TABLE items (
  id SERIAL PRIMARY KEY,
  embedding VECTOR(384)  -- For 384-dimensional vectors
);

-- Insert a vector
INSERT INTO items (embedding) VALUES ('[1,2,3,4,...]');

-- Find similar vectors (using L2 distance)
SELECT * FROM items ORDER BY embedding <-> '[1,2,3,4,...]' LIMIT 5;
```

### Creating an Index

For better performance with large datasets, create an index:

```sql
-- Create an HNSW index
CREATE INDEX ON items USING hnsw (embedding vector_l2_ops);

-- Or create an IVFFlat index
CREATE INDEX ON items USING ivfflat (embedding vector_l2_ops) WITH (lists = 100);
```

## Resource Management

The service is configured with the following resource limits:

- CPU: 0.5 cores
- Memory: 512MB

You can adjust these limits in the `docker-compose.yaml` file based on your needs.

## Networking

The service is configured to connect to an external network named `caddy_network`. This allows easy integration with a Caddy reverse proxy. If you're not using Caddy, you can modify the network configuration in the `docker-compose.yaml` file.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Additional Resources

- [pgvector GitHub Repository](https://github.com/pgvector/pgvector)
- [pgvector Documentation](https://github.com/pgvector/pgvector#readme)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
