# Microtask 6
Execute micro-mordred to obtain data from the study `enrich_geolocation` for any GitHub repository.

---

To excute the study `enrich_geolocation`, we need to add the following configurations to `setup.cfg`:

```json
[github]
raw_index = github_issues_chaoss
enriched_index = github_issues_chaoss_enriched
# update the token here
api-token = xxx
category = issue
sleep-for-rate = true
no-archive = true
sleep-time = 300
studies = [enrich_geolocation:user, enrich_geolocation:assignee]

[github:pull]
raw_index = github_pulls_chaoss
enriched_index = github_pulls_chaoss_enriched
# update the token here
api-token = xxx
category = pull_request
sleep-for-rate = true
no-archive = true
sleep-time = 300
studies = [enrich_onion:github, enrich_geolocation:user, enrich_geolocation:assignee]

[enrich_geolocation:user]
location_field = user_location
geolocation_field = user_geolocation

[enrich_geolocation:assignee]
location_field = assignee_location
geolocation_field = assignee_geolocation
```


