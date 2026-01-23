# Strapi Custom Image

Custom Docker image for Strapi with dynamic configuration generation based on environment variables.

## Quick Start

Build the custom Strapi image:

```bash
cd src/strapi/image
docker build -t strapi .
docker tag strapi localhost/strapi
```
