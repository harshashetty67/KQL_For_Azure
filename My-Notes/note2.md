### **Take Operator** :

```
//'take' operator => randomly picks given number of rows.
Perf
| take 10

// more 'take' queries => take helps in picking few rows out of thousand rows
Perf
| where TimeGenerated > ago(2h)
|
take 5

// 'take' has alias operator called 'limit' which does the same
Perf
| limit 10
```

===============================================================================

### **Count Operator**:

```
// Count => as the name says used for counting rows.

//Count total rows in Perf table
Perf
| count

// count with where clause
Perf
| where CounterValue > 90000
| count a
```

===============================================================================

### **Summarize :**

```
// 'summarize' => to summarize the content of table using aggregate functions like count() etc.
Perf
| summarize TotalRows = count()

// Summarize using a column name => Total is an alias name for column
Perf
| summarize Total=count() by Computer

// Using multiple columns
Perf
| summarize sum(CounterValue) by CounterName,InstanceName

// Combination of multiple aggregate functions.
Perf
| where CounterName == "% Processor Time"
| summarize
    TotalRows=count(),
    Sum=sum(CounterValue),
    Average = avg(CounterValue),
    Maximum = max(CounterValue),
    Minimum = min(CounterValue)
    by CounterName

// Using bin() => dividing the rows into buckets based on bin-size (second param) => here every 2 days count
Perf
| where TimeGenerated > ago(7d)
| summarize Total = count() by bin(TimeGenerated,2d)

// sorting the results => by default sort is desc
Perf
| where TimeGenerated > ago(7d)
| summarize Total = count() by bin(CounterValue,10)
| sort by CounterValue asc

```
