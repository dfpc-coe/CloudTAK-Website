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

2. Navigate to the desired install directory, in this guide we will assume the Home directory of the user.
    While CloudTAK can be installed using `root`, it is not recommended for security reasons and a non-root user should be used.

    ```
    cd ~/
    ```

3. Clone the CloudTAK Repository

    ```
    git clone https://github.com/dfpc-coe/CloudTAK.git
    ```

4. Navigate into the new git Directory created in the last step

    ```
    cd CloudTAK
    ```

5. Install necessary system dependencies

    ```
    ./cloudtak.sh install
    ```

6. Edit the Environment Variable file:

    ```
    nano .env
    ```

???+ warning

    Set `SigningSecret` and `MediaSecret` to secure values. These should be long, random strings.
    Leaving these values with the defaults can allow an attacker to gain access to your system.
    And generate valid authentication tokens without a user account.

    - Set `API_URL=https://map.<yourdomain>` IE: `https://map.cotak.gov`
    - Set `PMTILES_URL=https://tiles.map.<yourdomain>` IE: `https://tiles.map.cotak.gov`

The remaining Env Vars can be updated for an advanced deployment but the defaults will work for most.

7. Update your DNS configuration to create `A` records pointing to your CloudTAK Server's IP Address:

    - `A map.<yourdomain> => <CloudTAK Server IP>`
    - `A tiles.map.<yourdomain> => <CloudTAK Server IP>`

8. Start the Docker Containers

```
./cloudtak.sh start
```

9. Subsequent CloudTAK Updates can be performed with:

```
./cloudtak.sh update
```

The script will prompt to perform a Database Backup before proceeding with the update.
We highly recommend performing a backup while updating.

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

4. Restart the Docker Containers with the latest images

    ```
    docker compose up -d
    ```

## AWS Deployment
