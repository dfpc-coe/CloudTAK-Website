# CloudTAK Deploy

## Introduction

CloudTAK is designed to be deployed into one of two different environments; a full AWS deployment
via provided Infrastructure as Code (IaC) templates, or into a on-prem or alternate cloud environment
via provided Docker Compose files.

## Docker Compose Deployment (Single Server)

The following instructions will guide you through deploying CloudTAK using Docker Compose

The following are pre-requisites for a Docker Compose deployment:

- Working TAK Server
- TAK Server Admin Credentials
- Linux Distribution (Ubuntu 24.04+ recommended)

Note: commands below assume Ubuntu

1. Ensure Ubuntu Version is 24.04 or greater

    ```
    lsb_release -a
    ```

2. Install Docker and Docker Compose

    Follow the [Docker Provided instructions](https://docs.docker.com/engine/install/ubuntu/)

3. Install Git, Curl and Caddy

    ```
    sudo apt update
    sudo apt install -y git curl caddy
    ```

4. Clone the CloudTAK Repository

    ```
    git clone https://github.com/dfpc-coe/CloudTAK.git
    ```

5. Navigate to the Docker Compose directory

    ```
    cd CloudTAK
    ```

6. Build the Docker Containers

    ```
    docker compose build
    ```

7. Update Env Vars within the Docker Compose File

## AWS Deployment
