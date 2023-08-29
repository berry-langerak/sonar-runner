# Sonarqube runner

This is a simple Docker compose configuration to run Sonarqube on any arbitary
code base.

First, start the sonarqube service by running `docker compose up -d`. Log into
sonarqube running on http://localhost:9000 with the credentials admin/admin.
Create the project, and copy the token.

Then, run the scanner, while mounting the source:

```
TOKEN=<PROJECT_TOKEN>
PROJECT_KEY=<PROJECT_KEY>
SOURCE_DIR=<SOURCE_DIR>

docker compose run \
    --rm \
    -e SONAR_LOGIN="$TOKEN" \
    -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=$PROJECT_KEY" \
    -v "$SOURCE_DIR:/usr/src" \
    scanner
```

And wait until the scan is complete. The results are then visible in the
sonarqube admin interface.

