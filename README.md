# logzio-docker-ecs

logzio-docker-ecs collects logs from Amazon Elastic Container Service (ECS) and forwards them to Logz.io.
The container uses Fluentd to collect logs and fluent-plugin-detect-exceptions to collect stack traces.
fluent-plugin-detect-exceptions is a Fluentd plugin that detects stack traces in your logs and concatenates them.

To use this container, you'll set environment variables in your `docker run` command.
logzio-docker-ecs mounts docker.sock and the Docker logs directory to the container, allowing Fluentd to collect the logs and metadata.

## logzio-docker-ecs setup

### 1. Pull the Docker image

Download the logzio/logzio-docker-ecs image:

```shell
docker pull logzio/logzio-docker-ecs
```

### 2. Run the Docker image

For a complete list of options, see the parameters below the code block.👇

```shell
docker run logzio/logzio-docker-ecs \
--name=logzio-docker-ecs \
-e "LOGZIO_URL_1=https://<LISTENER-URL>:8071?token=<ACCOUNT-TOKEN>" \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /var/lib/docker/containers:/var/lib/docker/containers \
-v /tmp:/tmp \
-d --net="host"
```

#### Parameters

| Paramater | Details |
|---|---|
| **LOGZIO_URL_1** | **Required**. Your Logz.io listener URL and account token. To ship to different accounts, increment the number (e.g., `LOGZIO_URL_2`, `LOGZIO_URL_3`). <br /> Replace `<LISTENER-URL>` with your region's listener URL. For more information on finding your account's region, see [Account region](https://docs.logz.io/user-guide/accounts/account-region.html) in the Logz.io Docs. <br /> Replace `<ACCOUNT-TOKEN>` with the [token](https://app.logz.io/#/dashboard/settings/general) of the account you want to ship to. |

### 3. Check Logz.io for your logs

Spin up your Docker containers if you haven’t done so already. Give your logs some time to get from your system to ours, and then open [Kibana](https://app.logz.io/#/dashboard/kibana).
