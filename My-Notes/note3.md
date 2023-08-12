### **Extend** :

Extend operator helps in adding new columns.

```
// Extend => adding a new column

Perf
| where CounterName == "restartTimeEpoch"
| take 20
| extend Memory_In_MB = round(CounterValue/1024,0), Memory_In_GB = round(CounterValue/(1024*1024),0)

// Extend on string type column => string concatenation
Perf
| where ObjectName == "K8SContainer"
| take 5
| extend FQDName = strcat(Type," - ",ObjectName)
```

===============================================================

### **Project :**

Project operator helps in selecting subset of columns from the table

```
// 'Project' operator
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 10
| project Type,ObjectName,CounterName,CounterValue,CounterPath

// 'Project' with 'extend'
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 10
| extend Heading = strcat(Type, " : ", ObjectName), Memory_In_Gb = CounterValue / (1024 * 1024)
| project Type, ObjectName, CounterName, CounterValue, CounterPath

// Combining extend with project itself
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 5
| project
    Heading = strcat(Type, " : ", ObjectName),
    Type,
    ObjectName,
    CounterName,
    CounterValue,
    CounterPath,
    Memory_In_Gb = CounterValue / (1024 * 1024)
```

============================================================================

### **Variants of Project Operator** :

```
//project-away => excludes the columns from the result dataset/table
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 5
| project-away Type, ObjectName

// project-rename => renames a column
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 5
| project-rename Path = CounterPath
| project Computer, ObjectName, Path, Path_Length = strlen(Path)

// project-keep => projects the column in the order they occur in the source table
// Note: wildcard can be used for preseving a column -> Counter* returns every column starting with 'Counter'
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 5
| project-keep Computer,Counter*,TimeGenerated,InstanceName

// project-reorder -> helps in ordering the columns we need, then the rest column appears
// we can use asc/desc and wildcards too with project-reorder
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 5
| project-reorder _BilledSize,Computer,Counter* asc

// ordering every column in ascending order
Perf
| where CounterName == "memoryWorkingSetBytes"
| take 5
| project-reorder * asc

```
