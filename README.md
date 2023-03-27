# Docker Compose

Das folge würde ich dann anpasse für die entsprechende anwendung

version: '3.8'

services:
  frontend:
    image: your-frontend-image
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - my-network

  backend:
    image: your-backend-image
    build: ./backend
    ports:
      - "8080:8080"
    depends_on:
      - db
    environment:
      DB_HOST: db
    networks:
      - my-network

  db:
    image: postgres:13
    container_name: db
    environment:
      POSTGRES_USER: your-db-user
      POSTGRES_PASSWORD: your-db-password
      POSTGRES_DB: your-db-name
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - my-network

networks:
  my-network:
    driver: bridge

volumes:
  db-data:
