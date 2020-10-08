openshift olm apps
------------------

Topics

* Openshift OLM
* Cluster Logging Operator
* Elasticsearch Operator
* Elasticsearch
* Kibana
* Fluentd
* OpenShift Serverless Operator
* Knative
* Build your own Knative App

operator lifecycle manager
--------------------------

In OpenShift Container Platform 4.5, Operator Lifecycle Manager (OLM) helps users install, update, and manage the lifecycle of all Operators and their associated services running across their clusters. It is part of the Operator Framework, an open source toolkit designed to manage Kubernetes native applications (Operators) in an effective, automated, and scalable way.

Navigate to Administrator -> Operators -> Operator Hub

Take this time to review the many community and official Red Hat supported operators.

* [Concepts](https://docs.openshift.com/container-platform/4.5/operators/understanding_olm/olm-understanding-olm.html)

cluster logging
---------------

As a cluster administrator, you can deploy cluster logging to aggregate all the logs from your OpenShift Container Platform cluster, such as node system audit logs, application container logs, and infrastructure logs. Cluster logging aggregates these logs from throughout your cluster and stores them in a default log store. You can view the logs in a console or the OpenShift Container Platform web console or use Kibana to visualize log data.

Using Elasticsearch/Kibana to view your logs instead of the command line or web console can make it sigficantly easier to view logs across all of your pods or even namespace.

* [About](https://docs.openshift.com/container-platform/4.5/logging/cluster-logging.html)
* [Installation](https://docs.openshift.com/container-platform/4.5/logging/cluster-logging-deploying.html)

elasticsearch
-------------

Elasticsearch is a highly scalable open-source full-text search and analytics engine. It allows you to store, search, and analyze big volumes of data quickly and in near real time. It is generally used as the underlying engine/technology that powers applications that have complex search features and requirements. Elasticsearch provides a distributed system on top of Lucene StandardAnalyzer for indexing and automatic type guessing and utilizes a JSON based REST API to refer to Lucene features.

* [Overview](https://towardsdatascience.com/an-overview-on-elasticsearch-and-its-usage-e26df1d1d24a)

kibana
------

Kibana is a visual interface tool that allows you to explore, visualize, and build a dashboard over the log data massed in Elasticsearch Clusters.

* [Overview](https://www.clariontech.com/platform-blog/what-is-kibana-used-for-10-important-features-to-know)
* [Product Page](https://www.elastic.co/guide/en/kibana/current/introduction.html)

fluentd
-------

Fluentd is an open source data collector, which lets you unify the data collection and consumption for a better use and understanding of data. In the current setup it collects logs from all of the containers and forwards them to Openshift.

Fluentd tries to structure data as JSON as much as possible: this allows Fluentd to unify all facets of processing log data: collecting, filtering, buffering, and outputting logs across multiple sources and destinations (Unified Logging Layer). The downstream data processing is much easier with JSON, since it has enough structure to be accessible while retaining flexible schemas.

* [Architecture](https://www.fluentd.org/architecture)

kibana exercise
---------------

Log into Kibana and perform these basic tasks to get an understanding:

* Adjust the log columns by adding fields from the sidebar (the message column is usually a good start)
* Use the filter feature at the top left to find all the logs from a single namespace
* Adjust the time window top right to see logs from different times

openshift serverless operator
-----------------------------

Knative Serving on OpenShift Container Platform enables developers to write cloud-native applications using serverless architecture. Serverless is a cloud computing model where application developers don’t need to provision servers or manage scaling for their applications. These routine tasks are abstracted away by the platform, allowing developers to push code to production much faster than in traditional models.

Install Openshift Serverless operator and Knative Serving in preparation for creating a serverless app.

Once the cluster has cluster has Knative Serving installed create a [sample app](https://docs.openshift.com/container-platform/4.5/serverless/serving-creating-managing-apps.html).

* [Serverless](https://www.redhat.com/en/topics/cloud-native-apps/what-is-serverless)
* [Installing Operator](https://docs.openshift.com/container-platform/4.5/serverless/installing_serverless/installing-openshift-serverless.html)
* [Installing Knative Serving](https://docs.openshift.com/container-platform/4.5/serverless/installing_serverless/installing-knative-serving.html#installing-knative-serving)
* [Installing Knative Eventing](https://docs.openshift.com/container-platform/4.5/serverless/installing_serverless/installing-knative-eventing.html)

knative
-------

Knative focuses on three key categories: building your application, serving traffic to it, and enabling applications to easily consume and produce events.

In particular we will focus on Knative serving. Allows automatic scaling based on load, including scaling to zero when there is no load. Allows you to create traffic policies for multiple revisions, enabling easy routing to applications via URL.

Builds in Openshift are already handled by the integrated Build system covered in previous lessons.

Knative eventing is an amazing tool for responding to events. It's a more involved topic and we may cover it if we have more time.


* [Knative](https://knative.dev/)
* [Docs](https://knative.dev/docs/)
* [Getting Started](https://www.oreilly.com/library/view/getting-started-with/9781492047025/ch01.html)


build your own serverless app with knative
------------------------------------------

Now that you have a good overview of what knative can do create your own app from scratch and deploy it via a Knative service. Be sure to create your own namespace before starting.

Challenges:

* Write your server in any language.
    * It must service an http request on port 8080
    * It must allow overiding the default 8080 port with the PORT environment variable
* Bundle your service with a Dockerfile
* Using the knowledge gained in this course turn the Dockerfile into an image that the cluster can consume.
    * Example build options
    * Openshift Builds from github repo
    * Push to DockerHub
    * Push to Quay.io
* Create a knative service that consumes the image accessible to the cluster
    * Options
    * Use the kn CLI tool
    * Use the Openshift Serverless UI console
    * oc apply the knative service yaml

Once your service is up and running use Kibana to find the logs generated by your application.

* [Official Knative example application](https://knative.dev/docs/serving/samples/hello-world/helloworld-go/)

