# Deployment

Build the image

```shell
cd ${PROJECT_ROOT}
docker build . -t mindoc-ng
```

First run the docker-compose with 9th and 10th line commented in `docker-compose.yaml`

```yaml
version: '3'
services:
  app:
    container_name: mindoc-app
    image: mindoc-ng
    privileged: false
    restart: always
    volumes:
      # - ./mindoc-db:/mindoc/database/
      - ./mindoc-uploads:/mindoc/uploads/
      # - ./mindoc-conf:/mindoc/conf/
    networks:
      - default
    environment:
      - MINDOC_DB_DATABASE=/mindoc/database/mindoc.db 
      - MINDOC_ENABLE_EXPORT=true
      - MINDOC_BASEURL={yourbaseurl}
      - MINDOC_CACHE_PROVIDER=file
      - MINDOC_CACHE=true
      # - MINDOC_BASE_URL=
      # - MINDOC_CDN_IMG_URL=
      # - MINDOC_CDN_CSS_URL=
      # - MINDOC_CDN_JS_URL=
```

Attach to the container's shell, copy `/mindoc/database/` to `./mindoc-db` and `/mindoc/conf/` to `./mindoc-conf`.

Finally, uncomment the lines, and deploy the service for production

```yaml
version: '3'
services:
  app:
    container_name: mindoc-app
    image: mindoc-ng
    privileged: false
    restart: always
    volumes:
      - ./mindoc-db:/mindoc/database/
      - ./mindoc-uploads:/mindoc/uploads/
      - ./mindoc-conf:/mindoc/conf/
    networks:
      - default
    environment:
      - MINDOC_DB_DATABASE=/mindoc/database/mindoc.db 
      - MINDOC_ENABLE_EXPORT=true
      - MINDOC_BASEURL={yourbaseurl}
      - MINDOC_CACHE_PROVIDER=file
      - MINDOC_CACHE=true
      # - MINDOC_BASE_URL=
      # - MINDOC_CDN_IMG_URL=
      # - MINDOC_CDN_CSS_URL=
      # - MINDOC_CDN_JS_URL=
```