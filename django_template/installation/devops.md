# DevOps Setup

This document will explain DevOps setup and utilities for Django project
template.

## Docker Containers

- Build and run the entire application: `make build`
- Build and run the Django WSGI server: `make wsgi`
- Build and run the Django ASGI server: `make asgi`
- Build and run the PostgreSQL database: `make db`
- Build and run the Redis caching database: `make redis`
- Build and run the Celery Worker queue-consumer: `make celery-worker`
- Build and run the Celery Beat periodic tasks: `make celery-beat`
- Build and run the Celery Flower monitoring application: `make celery-flower`
- Build and run the Nginx for network reverse proxy: `make nginx`
- Start all the applications: `make start`
- Stop all the applications: `make stop`

## Django Server

## Celery Queue

## Local Testing
