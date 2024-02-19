# Refresh

Elasticsearch by default would update its index once per second, which can be configured using `refresh_interval` flag.

As a consequence, If we need to access the data right after the update/index, we can not get the lasted data. To make the index/update happen immediately, we can set the `refresh` flag.
