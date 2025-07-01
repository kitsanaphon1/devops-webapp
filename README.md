# devops-webapp


version: '3.8'

services:
  api:
    build:
      context: ./WebApiProject
      dockerfile: Dockerfile
    image: api-unittest:latest



     webapi:
    image: sooyaa02/noteapi:1.0
    build:
      context: ./WebApiProject
      dockerfile: Dockerfile
    container_name: webapi_container