# Setting up Dashboards

Metrics should be a key part of your DevOps process. It is through these metrics, one can drive continuous improvement of your delivery process. Almost all commands in sfpowerscripts, are instrumented. sfpowerscripts support various mechanisms to help you ingest the metrics into your preferred observability platform.

## Getting started with

### Stats D

* Ensure you have a StatsD Daemon running on a server, Setting up StatsD daemon on a server is quite simple, there are lot of guides available ([https://www.scalyr.com/blog/statsd-measure-anything-in-your-system/](https://www.scalyr.com/blog/statsd-measure-anything-in-your-system/)) . If you are after a hosted StatsD, hosted Graphite offers a hosted StatsD solution as part of their Hosted Graphite offering ([https://www.hostedgraphite.com/docs/integrationguide/ig\_hosted\_statsd.html](https://www.hostedgraphite.com/docs/integrationguide/ig\_hosted\_statsd.html)).
* Ensure your build agents can reach the StatsD server, this can be bit problematic, when you are using cloud based agents, which imply StatsD service has to be on the internet and reachable from the agent, so plan this out. If you are using self hosted agents, the StatsD server should be reachable as well.
* To visualize these metrics, you need a StatsD Backend ([https://thenewstack.io/collecting-metrics-using-statsd-a-standard-for-real-time-monitoring/](https://thenewstack.io/collecting-metrics-using-statsd-a-standard-for-real-time-monitoring/)) such as DataDog (Hosted), Graphana, and many others to aggergate and report data.
* Enable StatsD metrics in your scripts by adding these environment variables

```
 # Set STATSD Environment Variables for logging metrics about this build
 export SFPOWERSCRIPTS_STATSD=true
 export SFPOWERSCRIPTS_STATSD_HOST=172.23.95.52 
 export SFPOWERSCRIPTS_STATSD_PORT=8125     // Optional, defaults to 8125 
 export SFPOWERSCRIPTS_STATSD_PROTOCOL=UDP  // Optional, defualts to UDP, Supports UDP/TCP
```

### Log Based Metrics

sfpowerscripts is also able to generate metrics in a log file. These metrics are written to **.sfpowerscripts/metrics.log** in your working directory. This log file after every run of a command could be send to a log aggregator for further analysis.

The JSON payload consist of the the following, name of the metric (**metric**), type of the metric such as count, guage or timers ( **type** ), timestamp (**timestamp**) and followed by tags pertaining to the particular metric (**tags**)

A sample metric is shown below

```
{"metric":"sfpowerscripts.build.scheduled.packages","type":"count","timestamp":1616475396815,"tags":{"package":"core-crm","type":"Unlocked","is_diffcheck_enabled":"true","is_dependency_validated":"true","pr_mode":"false"}
```

One could write a parse this file, and then send each individual entries to a logging system that allows JSON based logging.

### Native Datadog Integration

sfpowerscripts is also able to integrate into Datadog natively using HTTP/HTTPS integration. This feature allows one to directly post metrics to Datadog instance without using an intermittent StatsD server to aggregate metrics before reaching an analyzer.

To setup native DataDog integration, you need to set the following environment variables

```
 # Set DATADOG Environment Variables for logging metrics natively to DataDog
 export SFPOWERSCRIPTS_DATADOG=true
 export SFPOWERSCRIPTS_DATADOG_HOST=app.datadoghq.com // Or equivalent datadog region
 export SFPOWERSCRIPTS_DATADOG_API_KEY=<your api key> // Refer to datadog documentation
```

More detailed instruction on setting up in Datadog is described in the below link

{% content-ref url="data-dog.md" %}
[data-dog.md](data-dog.md)
{% endcontent-ref %}

### Native NewRelic Integration

sfpowerscripts is also able to integrate into NewRelic natively using HTTP/HTTPS integration. Similar to native DataDog integration, this feature allows one to directly post metrics to NewRelic without using an intermittent StatsD server to aggregate metrics before reaching an analyzer.

```
# Set NEWRELIC Environment Variables for logging metrics natively to NewRelic
 export SFPOWERSCRIPTS_NEWRELIC=true
 export SFPOWERSCRIPTS_NEWRELIC_API_KEY=<your api key> // Refer to newrelic documentation to generate an NEWRELIC INGEST KEY
```

More detailed instruction on setting up in NewRelic is described in the below link

{% content-ref url="new-relic.md" %}
[new-relic.md](new-relic.md)
{% endcontent-ref %}

### Native Splunk Integration

sfpowerscripts is also able to integrate into Splunk natively using HTTP/HTTPS integration. This feature allows one to directly post metrics to Splunk instance without using an intermittent StatsD server to aggregate metrics before reaching an analyzer.

To setup native Splunk integration, you need to set the following environment variables

```
 # Set SPLUNK Environment Variables for logging metrics natively to Splunk
 export SFPOWERSCRIPTS_SPLUNK=true
 export SFPOWERSCRIPTS_SPLUNK_HOST=https://splunk-hec.your.app.com:your-port/services/collector/event // Or equivalent splunk region
 export SFPOWERSCRIPTS_SPLUNK_API_KEY=<your api key> 
```

More detailed instruction on setting up in Splunk is described in the below link

{% content-ref url="https://github.com/dxatscale/dxatscale-guide/blob/april-23/implementing-your-ci-cd/dashboard-setup/splunk.md" %}
[https://github.com/dxatscale/dxatscale-guide/blob/april-23/implementing-your-ci-cd/dashboard-setup/splunk.md](https://github.com/dxatscale/dxatscale-guide/blob/april-23/implementing-your-ci-cd/dashboard-setup/splunk.md)
{% endcontent-ref %}
