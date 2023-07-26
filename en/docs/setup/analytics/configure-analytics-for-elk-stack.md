# Configure Analytics for ELK Stack

## Step 1 - Setup Enforcer

1. Open `values.yaml` file.

2. Set following config under `wso2.apk.dp.gatewayRuntime` section to enable analytics.

    ```yaml
    analytics:
      enabled: true
      type: "ELK"
    ```

    !!! Note
        Optionally, `logLevel`. By default, this config is set to `INFO`.

        ```yaml
        analytics:
          enabled: true
          type: "ELK"
          logLevel: "INFO"
        ```

3. Redeploy the enforcer with the changes in `values.yaml`.

## Step 2 - Setup Elasticsearch and Kibana

To configure Elasticsearch and Kibana on your Kubernetes cluster, you can refer to the official guide provided by Elastic. The guide includes instructions on deploying the necessary Helm charts for Elasticsearch and Kibana.

You can find the official guide for setting up the Elastic stack (Elasticsearch and Kibana) on Kubernetes at: [https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-stack-helm-chart.html](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-stack-helm-chart.html)

## Step 3 - Setup Logging agent 

For forwarding Kubernetes logs to Elasticsearch, you have the option to use any logging agent that supports this functionality. Two commonly used options are Filebeat and FluentBit.

   - Filebeat: If you choose Filebeat, you can set it up in your Kubernetes environment by following the official guide provided by Elastic. Filebeat is a lightweight log shipper that is part of the Elastic Stack. It can be configured to collect logs from your Kubernetes pods and forward them to Elasticsearch.

      Official guide for running Filebeat on Kubernetes: [https://www.elastic.co/guide/en/beats/filebeat/current/running-on-kubernetes.html](https://www.elastic.co/guide/en/beats/filebeat/current/running-on-kubernetes.html)

   - FluentBit: Alternatively, you can opt for FluentBit as your logging agent. FluentBit is an open-source and efficient log processor and forwarder. It is designed to work well with Kubernetes environments and can be used to collect and send logs to Elasticsearch.

      Official guide for running FluentBit on Kubernetes: [https://docs.fluentbit.io/manual/installation/kubernetes](https://docs.fluentbit.io/manual/installation/kubernetes)

## Step 4 - Invoke requests and view analytics logs in Kibana UI

1. Deploy some sample APIs to APK and invoke endpoints.
2. Go to Kibana UI and search for logs
3. Under Logs > Stream section you will be able to see a lot of logs from all the pods. To view the analytics logs search for 'apimatrics'

[![Kibana logs](../../assets/img/analytics/kibana-logs-view.png)](../../assets/img/analytics/kibana-logs-view.png)

