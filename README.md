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




    name: Build and Tag Docker Image

on:
  push:
    tags:
      - 'v*.*.*'  # Trigger เมื่อมีการ push tag ที่ตรงกับ pattern นี้

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: 🔄 Checkout Repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0  # จำเป็นสำหรับการดึง tag

      - name: 🏷️ Get Version from Tag
        id: get_version
        uses: battila7/get-version-action@v2

      - name: 🐳 Build Docker Image
        run: |
          docker build -t myapp:${{ steps.get_version.outputs.version-without-v }} .

      - name: 📤 Push Docker Image
        run: |
          docker push myapp:${{ steps.get_version.outputs.version-without-v }}