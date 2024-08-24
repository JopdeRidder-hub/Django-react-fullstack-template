# Fullstack Template

This repository provides a fullstack application template with a Django backend, a Vite React frontend, and Nginx for serving the application. It uses Docker and Docker Compose to manage the development and production environments.

## Directory Structure

```
fullstack-template/
├── backend/
│   └── Dockerfile
│   └── manage.py
│   └── ... # Django project files
├── frontend/
│   └── src/
│       ├── Dockerfile
│       ├── package.json
│       ├── pnpm-lock.yaml
│       └── ... # Vite React project files
└── Dockerfile
└── nginx.conf
└── docker-compose.yml
└── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- **Docker**: Ensure you have Docker installed on your machine. [Install Docker](https://docs.docker.com/get-docker/).
- **Docker Compose**: Install Docker Compose, which is included with Docker Desktop or available as a standalone tool. [Install Docker Compose](https://docs.docker.com/compose/install/).

### Setting Up

1. **Clone the Repository**

   ```bash
   git clone https://github.com/JopdeRidder-hub/fullstack-template.git
   cd fullstack-template
   ```

2. **Configure Environment Variables**

   Copy the example environment file and update the values with your configuration:

   ```bash
   cp .env.example .env
   ```

   Update the `.env` file with your specific environment settings, such as database credentials and secret keys.

3. **Configure Database Credentials**

   Open the `docker-compose.yml` file and update the database credentials in the `db` service section. For example:

   ```yaml
   db:
     image: postgres:15-alpine
     container_name: db
     volumes:
       - postgres_data:/var/lib/postgresql/data
     environment:
       POSTGRES_DB: your_db_name
       POSTGRES_USER: your_db_user
       POSTGRES_PASSWORD: your_db_password
     ports:
       - "5432:5432"
   ```

   Replace `your_db_name`, `your_db_user`, and `your_db_password` with your actual database name, username, and password.

4. **Build and Start the Containers**

   Run the following command to build and start all services:

   ```bash
   docker-compose up --build
   ```

   This command will build Docker images for the backend, frontend, and Nginx, and start the containers.

5. **Run Database Migrations**

   After starting the containers, apply database migrations:

   ```bash
   docker-compose exec backend python manage.py migrate
   ```

### Accessing the Application

- **Frontend**: Access the Vite React application at `http://localhost:3000`.
- **Backend**: The Django backend will be accessible at `http://localhost:8000`.

### Updating the Frontend

1. **Make Changes**: Modify the frontend application as needed.
2. **Rebuild Docker Image**: After making changes, you may need to rebuild the Docker image for the frontend:

   ```bash
   docker-compose build frontend
   ```

3. **Restart Containers**: Restart the frontend service to apply changes:

   ```bash
   docker-compose up frontend
   ```

### Updating the Backend

1. **Make Changes**: Modify the Django application as needed.
2. **Apply Migrations**: Apply any new database migrations:

   ```bash
   docker-compose exec backend python manage.py migrate
   ```

### Nginx Configuration

- **Nginx Dockerfile**: Modify the `nginx/Dockerfile` and `nginx/nginx.conf` as needed to fit your requirements.

### File Exclusions

The `.gitignore` file is set up to exclude IDE-specific files and common temporary files. Ensure that any files you need to be version-controlled are not excluded by the `.gitignore`.

## Troubleshooting

- **Logs**: Check logs for any issues:

  ```bash
  docker-compose logs
  ```

- **Permissions**: Ensure that all files and directories have the correct permissions and are accessible.

- **Dependencies**: If you encounter issues with dependencies, ensure they are correctly listed in `package.json` and `pnpm-lock.yaml`.

## Contributing

Feel free to contribute by submitting issues or pull requests. Please ensure that your changes are well-documented and tested.

## License

This project is licensed under the [MIT License](LICENSE).

---
