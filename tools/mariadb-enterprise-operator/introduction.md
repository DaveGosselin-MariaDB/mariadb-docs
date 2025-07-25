---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Introduction

MariaDB Enterprise Operator provides a seamless way to run and operate containerized versions of MariaDB Enterprise Server and MaxScale on Kubernetes, allowing you to leverage Kubernetes orchestration and automation capabilities. This document outlines the features and advantages of using Kubernetes and the MariaDB Enterprise Operator to streamline the deployment and management of MariaDB and MaxScale instances.

## What is Kubernetes?

Kubernetes is more than just a container orchestrator; it is a comprehensive platform that provides APIs for managing both applications and the underlying infrastructure. It automates key aspects of container management, including deployment, scaling, and monitoring, while also handling essential infrastructure needs such as networking and storage. By unifying the management of applications and infrastructure, Kubernetes simplifies operations and improves efficiency in cloud-native environments.

## Why Kubernetes?

Kubernetes brings several key benefits to the table when managing applications in a containerized environment:

* Standardization: Kubernetes relies on standard APIs for managing applications and infrastructure, making it easier to ensure uniformity across various environments. It acts as a common denominator across cloud providers and on-premises.
* Automation: Kubernetes APIs encapsulate operational best practises, minimizing the need for manual intervention and improving the efficiency of operations.
* Cost Effectiveness: Having an standarized way to manage infrastructure across cloud providers and automation to streamline operations, Kubernetes helps reducing the infrastructure and operational costs.

## What is a Kubernetes Operator?

Kubernetes has been designed with flexibility in mind, allowing developers to extend its capabilities through custom resources and operators.

<figure><img src="../.gitbook/assets/operator-overview.png" alt=""><figcaption></figcaption></figure>

In particular, MariaDB Enterprise Operator, watches the desired state defined by users via `MariaDB` and `MaxScale` resources, and takes actions to ensure that the actual state of the system matches the desired state. This includes managing compute, storage and network resources, as well as the full lifecycle of the MariaDB and MaxScale instances. Whenever the desired state changes or the underlying infrastructure is modified, the Operator takes the necessary actions to reconcile the actual state with the desired state.

Operational expertise is baked into the `MariaDB` and `MaxScale` APIs and seamlessly managed by the Operator. This includes automated backups, restores, upgrades, monitoring, and other critical lifecycle tasks, ensuring reliability in Day 2 operations.

## MariaDB Enterprise Operator Features

* Provision and Configure MariaDB and MaxScale Declaratively: Define MariaDB Enterprise Server and MaxScale clusters in YAML manifests and deploy them with ease in Kubernetes.
* High Availability with Galera: Ensure availability with MariaDB Enterprise Cluster, providing synchronous multi-master replication.
* Query and Connection-Based Routing with MaxScale: MaxScale provides query routing and connection load balancing for improved application performance.
* Cluster-Aware Rolling Updates: Perform rolling updates on MariaDB and MaxScale clusters, ensuring zero-downtime upgrades with no disruptions to your applications.
* Flexible Storage Configuration and Volume Expansion: Easily configure storage for MariaDB instances, including the ability to expand volumes as needed.
* Backup Management: Take, restore, and schedule backups with multiple storage types supported: S3, PVCs, and Kubernetes volumes.
* Policy-Driven Backup Retention: Implement backup retention policies with bzip2 and gzip compression.
* Target Recovery Time: Restore your database to the closest available backup based on a specified recovery time.
* Bootstrap New Instances: Initialize new MariaDB instances from backups, S3, or PVCs to quickly spin up new clusters.
* TLS Certificate Management: Issue, configure, and rotate TLS certificates and Certificate Authorities (CAs) for secure connections.
* Native Integration with cert-manager: Leverage [cert-manager](https://cert-manager.io/docs/), the de-facto standard for managing certificates in Kubernetes, to enable issuance with private CAs, public CAs and HashiCorp Vault.
* Prometheus Metrics: Expose metrics using the MariaDB and MaxScale Prometheus exporters.
* Native Integration with prometheus-operator: Leverage [prometheus-operator](https://github.com/prometheus-operator/prometheus-operator) to scrape metrics from MariaDB and MaxScale instances.
* Declarative User and Database Management: Manage users, grants, and logical databases in a declarative manner using Kubernetes resources.

{% include "https://app.gitbook.com/s/SsmexDFPv2xG2OTyO5yV/~/reusable/pNHZQXPP5OEz2TgvhFva/" %}

{% @marketo/form formId="4316" %}
