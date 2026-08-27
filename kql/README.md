# KQL queries

Import the three evidence CSVs as tables in a free Azure Data Explorer
cluster or Log Analytics demo workspace, named to match the queries below:

| CSV | Import as table |
|---|---|
| `evidence/cloudora_msgtrace_logs.csv` | `MsgTrace` |
| `evidence/cloudora_click_delivery_logs.csv` | `ClickDelivery` |
| `evidence/cloudora_entra_signin_logs.csv` | `SigninLogs` |

Run the queries in this order — each file builds toward the final
correlation:

1. `message-trace.kql` — delivery scope
2. `click-investigation.kql` — engagement scope
3. `signin-investigation.kql` — the core correlation, confirming compromise

Screenshots of query + results go in `../evidence/screenshots/08-kql-correlation.png`.
