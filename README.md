# Logz.io AWS ECS Collector

This integration uses Fluentd in a Docker container to forward logs from Amazon Elastic Container Service (ECS) to Logz.io.

To use Logz.io AWS ECS Collector, you'll set environment variables when you run the container.
The Docker logs directory and docker.sock are mounted to the container, allowing Fluentd to collect the logs and metadata.

## Setup

### 1. Pull the Docker image

Download the logzio/logzio-aws-ecs image:

```shell
docker pull logzio/logzio-aws-ecs
```

### 2. Run the Docker image

For a complete list of options, see the parameters below the code block.👇

```shell
docker run -d logzio/logzio-aws-ecs \
--name=logzio-aws-ecs \
--env LOGZIO_URL="https://<LISTENER-URL>:8071" \
--env LOGZIO_TOKEN="<ACCOUNT-TOKEN>" \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /var/lib/docker/containers:/var/lib/docker/containers \
-v /tmp:/tmp \
--net="host"
```

#### Parameters

| Paramater | Details |
|---|---|
| **LOGZIO_URL** | **Required**. Your Logz.io listener URL. Replace `<LISTENER-URL>` with your region's listener URL. For more information on finding your account's region, see [Account region](https://docs.logz.io/user-guide/accounts/account-region.html) in the Logz.io Docs. |
| **LOGZIO_TOKEN** | **Required**. Your Logz.io account token. Replace `<ACCOUNT-TOKEN>` with the [token](https://app.logz.io/#/dashboard/settings/general) of the account you want to ship to. |

### 3. Check Logz.io for your logs

Spin up your Docker containers if you haven’t done so already. Give your logs some time to get from your system to ours, and then open [Kibana](https://app.logz.io/#/dashboard/kibana).
