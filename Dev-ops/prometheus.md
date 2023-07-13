# Prometheus

Prometheus is a tool for monitoring services.

## How it works

Prometheus' data could be configured using metric endpoints to scrape the data.

* An application can provide the metric enpoint with the help of `client libraries` that support multiple languges.
* Without the help of client libraries, we can use `exporter` which will gather metrics from specific applications (clound, database, hardware machine, etc)
* The endpoint can also be provied via the service discovery that help to obtains endpoint automatically. E.g. the Kubenates API returns the endpoint for pods and nodes metrics.

For storing the data, prometheus only keep the data for 15 days in default rather than keeping all of them.
We can also config a remote storage via remote_write and remote_read endpoints as a backup.
Prometheous would regulary send data to remote_write and read data from remote_read then combine it with existing data. 

To visualize the data, Prometheus also frondend UI or we can integrate with other visualize tool like Grafana.