# Strapi Custom Image

Custom Docker image for Strapi with dynamic configuration generation based on environment variables.

## Quick Start

Build the custom Strapi image:

```bash
cd src/strapi/image
docker build -t strapi .
docker tag strapi localhost/strapi
```

## Building with Specific Version

You can build the image with a specific version of Strapi from npm:

```bash
# Using latest version (default)
docker build -t strapi:latest .

# Using a specific version
docker build --build-arg STRAPI_VERSION=5.6.0 -t strapi:5.6.0 .

# Using beta version
docker build --build-arg STRAPI_VERSION=5.7.0-beta.1 -t strapi:beta .
```

Note: The Dockerfile uses yarn for package management, so the final image will use yarn to run the application.
