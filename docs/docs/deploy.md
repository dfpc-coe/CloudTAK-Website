# CloudTAK Deploy

## Introduction

CloudTAK is designed to be deployed into one of two different environments; a full AWS deployment
via provided Infrastructure as Code (IaC) templates, or into a on-prem or alternate cloud environment
via provided Docker Compose files.

## Docker Compose Deployment

### Initial Install & Setup

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

4. Navigate to the desired install directory, in this guide we will assume the Home directory of the user.
    While CloudTAK can be installed using `root`, it is not recommended for security reasons and a non-root user should be used.

    ```
    cd ~/
    ```

5. Clone the CloudTAK Repository

    ```
    git clone https://github.com/dfpc-coe/CloudTAK.git
    ```

6. Navigate to the Docker Compose directory

    ```
    cd CloudTAK
    ```

7. Update Env Vars within the provided Env File, using the .env file

    ```
    mv example.env .env
    ```

8. Build the Docker Containers

    ```
    docker compose build
    ```

9. Start the Docker Containers

    ```
    docker compose up -d
    ```

### Updating CloudTAK or Docker Compose Configuration

1. Navigate to the CloudTAK directory

    ```
    cd CloudTAK
    ```

2. Ensure you are on the desired branch, for production ready releases, use the `main` branch

    ```
    git branch # Print the current branch
    git checkout main # Switch to the main branch if not already on it
    ```

2. Pull the latest changes from the repository

    ```
    git pull
    ```

3. Rebuild the Docker Containers

    ```
    docker compose build api --no-cache
    docker compose build events
    docker compose build tiles
    docker compose build media
    ```

4. Restart the Docker Containers

    ```
    docker compose up -d
    ```

## AWS Deployment
