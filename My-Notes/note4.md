### **Useful operators in KQL :**

1). Distinct :

Helps in selecting unique rows

Examples :

```
// distinct
Perf
| take 5
| distinct CounterName, ObjectName
| sort by CounterName asc, ObjectName asc

SigninLogs
| distinct ResultDescription

```

========================================

2). Top :

Top operator helps fetching first top rows from dataset.

```
// top
Perf
| top 10 by TimeGenerated desc

```

========================================

3). Print :

Prints the data passed to it.

```
// print - examples

print 5

print 100*5

print "Hello"

print strcat("hello","-","Tom")

// named printing
print Answer = 50*2

// date calculation
print ago(50d)
```
