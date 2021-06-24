# Package Guidelines
The purpose of this document is to establish a set of common guidelines that govern various aspects of the package creation process. 
By doing so contributors ensure that their work is relatively self-documenting and easy to extend or modify.

## General Guidelines

1. Object names should be alphanumeric and accept underscores in place of spaces.
2. Objects should be exported by type without enabling `Include related objects`. The following names are suggested:
    - config.ndjson
    - index-pattern.ndjson
    - url.ndjson
    - queries.ndjson
    - search.ndjson
    - visualization.ndjson
    - dashboard.ndjson
3. There must be at least one dashboard with general markdown documentation describing how to navigate your package.

## Saved Searches

1. The name should be lower-case and separated by underscores. 
2. The name should be descriptive describing both the filters operating against it as well as the information it is trying to convey.
> ⓘ Examples
> - zeek_layer_3_conversations_client_server
> - zeek_large_dns_zone_transfer_transactions
> - suricata_high_severity_alerts_local_orig

## Visualizations

1. The name should be lower-case and separated by underscores.
2. The name should be descriptive in nature, and be prefixed by the **type_** of visualization for easy searching when creating dashboards.
> ⓘ Valid prefixes 
> - area
> - controls
> - map
> - data_table
> - gantt_chart
> - gauge
> - goal
> - heat_map
> - bar
> - line
> - markdown
> - metric
> - pie / donut
> - tsvb
> - cloud
> - timelion
> - vega

> ⓘ Examples
> - donut_zeek_dns_transactions_by_r_code
> - tsvb_suricata_alerts_over_time
> - metric_tcp_connections

## Dashboards

1. The name of the dashboard should be capitalized and separated by spaces, as dashboards tend to be the most user-facing component.
2. The name of the dashboard should be intentionally short and related to the theme of the visualizations contained within.

> ⓘ Examples
> - Events
> - Alerts
> - Alert Maps
> - Conversations
> - Protocols
> - DNS Transactions

## Manifest
1. The manifest description must state the purpose of the package and the high-level use-cases it addresses.
2. The `file_list` parameter should be ordered as follows: `["config.ndjson", "index_patterns.ndjson", "url.ndjson", "query.ndjson", "searches.ndjson", "visualizations.ndjson", "dashboards.ndjson"]`
3. The `author_email` must be valid.
