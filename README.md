# AngularProxy
This project demonstrates how a http proxy can be added to an Angular application to connect to a backend service.

## Build the container image using build packs

```bash
pack build angular-proxy \
--buildpack paketo-buildpacks/web-servers \
--env BP_NODE_RUN_SCRIPTS=build \
--env BP_WEB_SERVER_ROOT=dist/angular-proxy \
--builder paketobuildpacks/builder:base
```

## Run the image

### Run the backend service

```bash
npx json-server --watch db.json --host 0.0.0.0
```

### Find the IP address of the host

```bash
ip a
```

### Run the built image

```bash
docker run --rm --name angular-proxy \
--env PORT=8080 \
--env BACKEND_HOST=<HOST IP ADDRESS> \
--env BACKEND_PORT=3000 \
--publish 8080:8080 angular-proxy
```
