# Microtask 3
Based on the JSON documents produced by Perceval and its source code, try to answer the following questions:

- What is the meaning of the JSON attribute `timestamp`?
  
  **The Unix timestamp that used to explain the datetime when the item was fetched from the data source.**

- What is the meaning of the JSON attribute `updated_on`?

  **The last time (Unix timestamp) the data was last updated.**

- What is the meaning of the JSON attribute `origin`?

  **The URL of the data source, e.g., Git repository.**

- What is the meaning of the JSON attribute `category`?

  **It includes the category of item to be fetched from the the data source.**

- How many categories do the Git and GitHub backends have?

  **As is shown in [microtask-2](../microtask-2):**
  - **`Git` has only one category: 'commit'.**
  - **`Github` has three categories, 'issue', 'pull_request', 'repository'.**
  

- What is the meaning of the JSON attribute `uuid`?

  **It is universally unique identifier (UUID), which will be the SHA1 of the concatenation of the values from the list.**

  - [grimoirelab-perceval/backend.py#L427](https://github.com/chaoss/grimoirelab-perceval/blob/805d73122b871c29146a70601d8f3d78267b41e1/perceval/backend.py#L427)

- What is the meaning of the JSON attribute `search_fields`?

  **It adds the values of the fields defined in `SEARCH_FIELDS` class attribute with their corresponding keys.**

  **In case of `Github`, It adds the values of `metadata_id` plus the `owner` and `repo`**.

  - [grimoirelab-perceval/backend.py#L277](https://github.com/chaoss/grimoirelab-perceval/blob/28d4b13fdeddaa43c89fd69a530242b1396208d6/perceval/backend.py#L277) 
  - [grimoirelab-perceval/github.py#L144](https://github.com/chaoss/grimoirelab-perceval/blob/28d4b13fdeddaa43c89fd69a530242b1396208d6/perceval/backends/core/github.py#L144)


- What is stored in the attribute `data` of each JSON document produced by Perceval?
 
  **The `data` store the information which are extracted from the data source using the Perceval Backends.**
  
  - **In case of `Git Commit`, please refer to [microtask-2.ipynb](../microtask-2/microtask-2.ipynb)**
  - **In case of `Github Issue`, please refer to [issue.json](../microtask-2/issue.json)**
  - **In case of `Github Pull Request`, please refer to [pull_request.json](../microtask-2/pull_request.json)**

- Identify the code in charge of dealing with remote APIs and explain its logic.

  **The function [*_fetch_from_remote()*](https://github.com/chaoss/grimoirelab-perceval/blob/fee51cd793131cdaa0a2e10d0f0183eed12fb995/perceval/client.py#L171) would be used to obtain data from the remote data source. This methord was implemented in the abstract class for HTTP clients -- `HttpClient`, so that sub-classes can use it to query data sources taking care of retrying requests in case connection issues.**

  **During the initialization of the specific client , a http session would be created by [*_create_http_session()*](https://github.com/chaoss/grimoirelab-perceval/blob/fee51cd793131cdaa0a2e10d0f0183eed12fb995/perceval/client.py#L193), which can provide cookie persistence, connection-pooling, and configuration. And then we can use `self.session.get()` or `self.session.post()` to send a request to remote API and return the `response` object.**


- Which is the folder that stores the archives generated by Perceval?

  **We can use `--archive-path` to specify the archive path in some cases. If not, the default archive path is `~/.perceval/archives/`. The function [*`create_archive()`*](https://github.com/chaoss/grimoirelab-perceval/blob/fee51cd793131cdaa0a2e10d0f0183eed12fb995/perceval/archive.py#L368) would create a brand new archive with a random SHA1 as its name. The first byte of the hashcode will be the name of the subdirectory and the remaining bytes will be the archive name.**