# PHP Docker Compose NewRelic APM

This repo holds a minimal PHP app in docker-compose that is instrumented by NewRelic's PHP APM.

## Getting Started

```sh
git clone https://github.com/briankopp/php-newrelic-agent
```

You'll need a couple of secrets, so create an `.env` file.

```sh
touch .env
echo "NEW_RELIC_LICENSE_KEY=[your_license_key_here]" >> .env
echo "NEW_RELIC_APP_NAME=test-php" >> .env
```

Build and run!

```sh
docker-compose build
docker-compose up
```

Open a browser to `http://localhost:8080/index.php`.

In a few minutes, your `test-app` php app will be present in APM.
