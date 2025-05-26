# Logstash boilerplate

This repository contains a boilerplate for deploying logstash on Scalingo.

You have three different configuration available:

* `logstash.conf`: this configuration will listen for http request
  authenticated by the authentication information passed in the `USER` and
  `PASSWORD` environment variables and send it to and OpenSearch database.
  This will also parse url defined variables.
* `logstash-json.conf` this configuration is based on the previous one but if
  the content is a valid json it will parse it
* `logstash-kv.conf` this configuration is based on `logstash.conf` but it will
  also parse the content to search and parse patterns like `key=value`


## Configuration

You will need to configure the following environment variables:

* `USER` the username that you will use to authenticate against your logstash
  instance
* `PASSWORD` the password that you will use to authenticate against your
  logstash instance
* `OPENSEARCH_HOST` the URL of the OpenSearch database
* `OPENSEARCH_USER` the username to access the OpenSearch database
* `OPENSEARCH_PASSWORD` the password to access the OpenSearch database

You will also change the `change-me` index name in the output section of your
logstash configuration.


## Updating Logstash version

To update your application with a more recent version of version of **Logstash**,
the most straightforward method is to deploy your application. The
[used buildpack](https://github.com/Scalingo/logstash-buildpack) is defining the
[used version](https://github.com/Scalingo/logstash-buildpack/blob/master/bin/compile#L9),
which can be overrided with the environment variable `LOGSTASH_VERSION`.

To trigger the new deployment, either use:

- The *Manual Deployment* feature of our GitHub or Gitlab
- `git push` deployment after adding an empty commit to your project:
  `git commit --allow-empty -m "New deployment to update logstash"`
