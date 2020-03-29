# Microtask 3
After reading the documentation at https://www.elastic.co/elastic-stack and https://opendistro.github.io/for-elasticsearch/ try to answer the following questions:

### What's an index?

An index is [defined](https://www.elastic.co/guide/en/elasticsearch/reference/current/glossary.html#index) as:
> An optimized collection of JSON documents. Each document is a collection of fields, the key-value pairs that contain your data.

> An index is a logical namespace that maps to one or more primary shards and can have zero or more replica shards.

In another words, An index is like a `database` in a relational database. We can think of an index like a database:
```
MySQL => Databases => Tables => Columns/Rows
Elasticsearch => Indices => Types => Documents with Properties
```

An Elasticsearch cluster can contain multiple `Indices` (`databases`), which in turn contain multiple `Types` (`tables`). These types hold multiple `Documents` (`rows`), and each document has `Properties`(`columns`).

### What's an index pattern?

An index pattern is [defined](https://www.elastic.co/guide/en/elasticsearch/reference/current/glossary.html) as:

> A string that can contain the `*` wildcard to match multiple index names. In most cases, the index parameter in an Elasticsearch request can be the name of a specific index, a list of index names, or an index pattern. For example, if you have the indices `datastream-000001`, `datastream-000002`, and `datastream-000003`, to search across all three you could use the `datastream-*` index pattern.

### What is stored in the index .kibana?

Kibana stores its objects as documents in the .kibana index in Elasticsearch.

### What is a tenant?

A Kibana `tenant` is a named container for storing saved objects (“space”). Different Kibana tenants are isolated from one another. 

When running multiple tenants of Kibana by changing the `kibana.index` in your `kibana.yml`, you cannot use `kibana_admin` to grant access. You must create custom roles that authorize the user for that specific tenant. Although multi-tenant installations are supported, the recommended approach to securing access to Kibana segments is to grant users access to specific spaces. For example, a tenant using `kibana.index: .kibana` will have its own set of roles created to grant access to Kibana. If you create another tenant at `kibana.index: .some-other-index`, it will need its own set of roles to grant access to that tenant.

### What's the difference between ElasticSearch and ODFE?

Open Distro for Elasticsearch is well-suited to the following use cases:
- Log analytics
- Real-time application monitoring
- Clickstream analytics
- Search backend

Compared to the open source distribution of Elasticsearch, Open Distro for Elasticsearch offers many extra features:

| Component |	Purpose |
|  ----  | ----  |
| Elasticsearch	| Data store and search engine |
| Kibana | Search frontend and visualizations |
| Security	| Authentication and access control for your cluster|
| Alerting | Receive notifications when your data meets certain conditions |
| SQL	| Use SQL to query your data |
| Index State Management |	Automate index operations |
| Performance Analyzer	| Monitor and optimize your cluster |
| Anomaly Detection	| Identify atypical data and receive automatic notifications |

Here is the [reference](https://opendistro.github.io/for-elasticsearch-docs/).

There's also a [decent explanation](https://aws.amazon.com/cn/blogs/opensource/keeping-open-source-open-open-distro-for-elasticsearch/) as to why Amazon is going down this path, a key line to take away:

> Unfortunately, since June 2018, we have witnessed significant intermingling of proprietary code into the code base. While an Apache 2.0 licensed download is still available, there is an extreme lack of clarity as to what customers who care about open source are getting and what they can depend on. For example, neither release notes nor documentation make it clear what is open source and what is proprietary. Enterprise developers may inadvertently apply a fix or enhancement to the proprietary source code. This is hard to track and govern, could lead to breach of license, and could lead to immediate termination of rights (for both proprietary free and paid). Individual code commits also increasingly contain both open source and proprietary code, making it very difficult for developers who want to only work on open source to contribute and participate. In addition, the innovation focus has shifted from furthering the open source distribution to making the proprietary distribution popular. This means that the majority of new Elasticsearch users are now, in fact, running proprietary software.

> As was the case with Java and OpenJDK, our intention is not to fork Elasticsearch, and we will be making contributions back to the Apache 2.0-licensed Elasticsearch upstream project as we develop add-on enhancements to the base open source software. In the first release, we will include many new advanced but completely open source features including encryption-in-transit, user authentication, detailed auditing, granular roles-based access control, event monitoring and alerting, deep performance analysis, and SQL support.

 