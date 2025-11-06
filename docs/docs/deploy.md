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

    If you are using the `cloudtak.sh` install script, then the `SigningSecret` & `MediaSecret`
    will be randomly generated for you. If you are not using the install script, you must
    set these values to be long, random strings. Leaving these values with the defaults can allow
    an attacker to gain access to your system and generate valid authentication tokens without a user account.

- Set `API_URL=https://map.<yourdomain>`

For Example: `API_URL=https://map.cotak.gov`

- Set `PMTILES_URL=https://tiles.map.<yourdomain>`

For Example: `PMTILES_URL=https://tiles.map.cotak.gov`

The remaining Env Vars can be updated for an advanced deployment but the defaults will work for most.

7. Update your DNS configuration to create `A` records pointing to your CloudTAK Server's IP Address:

    - `A map.<yourdomain> => <CloudTAK Server IP>`
    - `A tiles.map.<yourdomain> => <CloudTAK Server IP>`

8. Start the Docker Containers

```
./cloudtak.sh start
```

### Updating CloudTAK

1. Navigate to the CloudTAK directory

    ```
    cd CloudTAK
    ```

2. Run the provided CloudTAK Update Script

    ```
    ./cloudtak.sh update
    ```

    It will prompt you to perform a database backup before proceeding with the update, we recommend you always do so.

## DNS Configuration

Final DNS Configuration should have the following entries:

| Record Type | Hostname               | Points To                | Example                    |
| ----------- | ---------------------- | ------------------------ | -------------------------- |
| A           | <sub>.example.com      | CloudTAK API & Web UI    | map.example.com            |
| A           | <sub>.example.com      | CloudTAK Media Server    | video.example.com          |
| A           | tiles.<sub>.example.com| CloudTAK Tile Server     | tiles.map.example.com      |

Note that the relationship between subdomains in the tree is important as CloudTAK will automatically generate
Content Security Policy (CSP) headers that allow the API & Web UI to access the Media and Tile servers.

The following rules must be adhered to unless customizing the nginx configuration files directly:
- The API & Web UI must be on the same level subdomain (e.g. `map.example.com` & `video.example.com`)
- The Tile server must be on a subdomain of the API & Web UI (e.g. `tiles.map.example.com`) AND must be named `tiles`

## AWS Deployment

## S3 Bucket Configuration

CloudTAK will use a single S3 compatible store for storing assests including map tiles, user uploaded files, and other static content.

If you are using the provided AWS CloudFormation Or Docker Compose file, this bucket will be created for you. In AWS this will be created
with a native S3 bucket, while Docker Compose will deploy a `Minio` instance to provide S3 compatible storage.

The following key prefixes will be used within the S3 Bucket:

| Prefix                            | Management    | Description |
| --------------------------------- | ------------- | ----------- |
| `attachment/{sha256}/{file.ext}`  | Automated     | CoT Attachments by Data Package reported SHA |
| `import/{UUID}/{file.ext}`        | Automated     | Initial User File Uploads |
| `profile/{email}/{file.ext}`      | Automated     | User Files & Cloud Optimized outputs from Import process |
| `public/{name}.pmtiles`           | User Provided | Public Tile Pyramids |

### Public Tile Pyramids

Public Tile Pyramids are user provided PMTiles files that are made available to any authenticated CloudTAK User.

While the server will immediately host tile requests for any uploaded PMTiles file, for users to see the Tile source
in the UI, an entry must be created via the Admin Overlay Console and set to `Public` for users to have a UI
driven method for discovering and using the Tile source.
