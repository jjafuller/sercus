```yaml
schema: v1
id: region
name: Region
description: |
    ...
repo: github.com/jjafuller/region
build: jenkins...
release_strategy: blue/green
type: api
team: "jjaf"
on_call: ...
environments:
    - name: prd
      aliases: production, prod
	  host: aws-eb
environment_urls:
    - prd:
        - name: api
          url: ...
        - name: dashboard
          url: ...
        - name: management
          url: ...
monitoring_dashboard_urls:
	- name: primary
	  url: https://grafana.blue.production.govuk.digital/dashboard/file/email_alert_api.json?refresh=10s&orgId=1
    - name: sentry
	  url: https://sentry.io/govuk/find-data
doc:
	- name: guidebook
      url: ...
	  reviewed: 2020-08-31
      review_frequency: quarterly
	- name: runbook
	  url: ...
	  reviewed: 2020-09-30
      review_frequency: quarterly
dependencies:
    - currency
	- bonus
    - passion
```
