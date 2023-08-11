### Search operator:

// 'search' operator => kusto does case-insensitive search by default
Perf
| search "Memory"
| take 50

// For 'case-sensitive' search
Perf
| search kind=case_sensitive "memory"

// Only giving 'search' => searches in every single table in entire collection DB in the Azure data cluster
//Not recommended
search "Memory"

// search in group of tables
search in (Perf,AuditLogs,AzureActivity) "Memory"

// searching for exact match in specific column of a table => case-sensitive search
Perf
| search InstanceName == "Memory"

// same as above but searching for matching word in a column.
Perf
| search CounterName:"Memory"

// using wildcard _ for search
Perf
| search "Bytes_"

// startswith and endswith
Perf
| search \* startswith "linux"

// combining multiple condition
Perf
| search "Free*Bytes" and ("Bytes*" or "Linux")

// regex
Perf
| search \* matches regex "[A-Z]:"

### Where operator :

// 'where' operator => fetching rows based on a condition
Perf
| where TimeGenerated > ago(5h) and CounterValue > 1000000

// using startswith/endswith with 'where' just like 'search'
Perf
| where \* endswith "Bytes"

// using wildcard search => we dont use _ in where operator
Perf
| where _ has "Linux"

//Regex
Perf
| where \* matches regex "[0-9]"
