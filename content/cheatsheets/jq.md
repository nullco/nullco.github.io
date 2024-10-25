+++
author = "null.co"
title = "jq Cheatsheet"
date = "2024-10-25"
description = ""
tags = [
    "cheatsheet",
    "jq",
]
categories = [
    "cheatsheet"
]
aliases = ["cheatsheet"]
+++

By default jq reads from *STDIN* a stream of JSON inputs (whitespace-separated values). It processes each input with the jq program (filters) specified at the command line, and prints the outputs of processing each input with the program to *STDOUT*.

```bash
echo '"hello" 123 ["one", "two", "three"] { "name": "jq" }' | jq '.'
```
For each input, by default its output is:
- pretty-printed
- separated from other outputs by `\n`.

The `.` means identity operator, which just referes to entire input 

To combine input values into one single input array:

```bash
echo '1 "two" 3' | jq -s .
```

To pass values as arguments to jq, and use them inside the program:

```bash
jq -n --arg val 123 '$val'
```
For JSON arguments:

```bash
jq -n --argjson val 123 '$val'
```

*Note*: -n argument means "Don't read any input at all".

To use reuse key/value from input:

```bash
jq -n '{"c": 3} | {"a": 1, "b", "c"}'
```

Using pipes:

```bash
jq -n '1 | . + 2 | . + 3'
```

Accessing arrays:

```bash
jq -n '["Peter", "Jerry"][1]'            # => "Jerry"
jq -n '["Peter", "Jerry"][-1]'           # => "Jerry"
jq -n '["Peter", "Jerry", "Tom"][1:]'    # => ["Jerry", "Tom"]
jq -n '["Peter", "Jerry", "Tom"][:1+1]'  # => ["Peter", "Jerry"]
jq -n '["Peter", "Jerry", "Tom"][1:99]'  # => ["Jerry", "Tom"]
```
If index / key is ommitted, then one output is generated for each value in the array/object

```bash
jq -n '[1, 2, 3] | .[]'
jq -n '{a: 1, b: 2, c: 3}[]'
```

Selecting values:
```bash
jq -n '1, 2, 3, 4, 5 | select(. % 2 != 0)'

# Output
# 1
# 3
# 5
```

## Examples

transform file into another shape

```bash
jq '{user_id: 1, documents: .data.documents | map({docdb_family_id: .general.docdb_family_id})}' search_response.json

jq '{user_id: 1, documents: [.data.documents[] | {docdb_family_id: .general.docdb_family_id}]}' search_response.json

```

Select elements from array matching condition:

```bash
jq '.data.documents[] | .general.docdb_family_id | select(. % 10 == 8)' search_response.json
```
Update assignment
```bash
jq '.data.documents |= map(select(.general.docdb_family_id % 10 == 8))' search_response.json
```

Match regular expression inside string and capture group
```bash
jq 'match("run-(\\d+)").captures[0].string' -r All-Messages-search-result.csv
```
