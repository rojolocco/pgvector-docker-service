# PostgreSQL Docker Service

This project provides a Docker setup for running PostgreSQL and pgAdmin, a web-based interface for managing PostgreSQL databases.

## Description

This repository contains Docker configurations to easily deploy PostgreSQL and pgAdmin. PostgreSQL is a powerful, open-source object-relational database system. pgAdmin allows you to manage your PostgreSQL databases through a user-friendly web interface.

## Services

- **PostgreSQL**: The main service that runs the PostgreSQL database.
  - **Container Name**: postgres
  - **Image**: postgres
  - **Ports**: Exposed on the default PostgreSQL port (5432)
  - **Volumes**: Data is persisted in `postgres_data` volume.
  - **Health Check**: Ensures PostgreSQL is running by checking the readiness of the server.

- **pgAdmin**: A web interface for managing PostgreSQL.
  - **Container Name**: pgadmin
  - **Image**: dpage/pgadmin4:latest
  - **Ports**: Accessible on port 8082
  - **Environment Variables**: Loaded from `.env`

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/your-repo.git
   ```

2. Navigate to the project directory:

   ```bash
   cd your-repo
   ```

3. Start the services using Docker Compose:

   ```bash
   docker-compose up -d
   ```

## Usage

- Access pgAdmin at [http://localhost:8082](http://localhost:8082) to manage your PostgreSQL databases.
- Use any PostgreSQL client to connect to the PostgreSQL service at `localhost:5432`.

## Contributing

1. Fork the repository.
2. Create a new branch:

   ```bash
   git checkout -b feature/YourFeature
   ```

3. Make your changes and commit them:

   ```bash
   git commit -m "Add your message"
   ```

4. Push to the branch:

   ```bash
   git push origin feature/YourFeature
   ```

5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
