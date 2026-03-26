jq
===

A lightweight and flexible command-line JSON processor.

## Description

`jq` is a lightweight and flexible command-line JSON processor. It is used to parse, filter, and transform JSON data. It applies filters to its JSON input and produces results as JSON on standard output.

The simplest filter is `.`, which copies the input to the output without modification (formatting it nicely).

`jq` currently supports 64-bit double-precision floating-point numbers (IEEE754).

### Installation

For Debian/Ubuntu:
```bash
sudo apt-get install jq
```

For RedHat/CentOS:
```bash
sudo yum install jq
```

### Syntax

```bash
jq [options] <jq filter> [file...]
jq [options] --args <jq filter> [strings...]
```

### Options

```bash
-c               Compact output (one line per object).
-n               Use `null` as the single input value.
-e               Set exit status based on the output.
-s               Slurp: Read all inputs into an array before applying the filter.
-r               Output raw strings instead of JSON texts.
-R               Read raw strings instead of JSON.
-C               Enable colorized output.
-M               Monochrome (no colors).
-S               Sort object keys alphabetically.
--tab            Use tabs for indentation.
--arg k v        Set variable $k to value v.
```

### Examples

**Pretty print JSON:**
```bash
echo '{ "foo": { "bar": { "baz": 123 } } }' | jq '.'
```

**Get a value by key:**
```bash
echo '{"foo": 42}' | jq '.foo'
# Output: 42
```

**Array operations:**
```bash
echo '[{"name":"JSON"}, {"name":"XML"}]' | jq '.[1]'
```

**Construct new objects:**
```bash
echo '{"user":"root","titles":["admin", "super"]}' | jq '{user, role: .titles[]}'
```

**Calculate length:**
```bash
echo '[1, 2, 3]' | jq 'length'
# Output: 3
```

**Pipe filters:**
```bash
echo '[{"name":"JSON"}, {"name":"XML"}]' | jq '.[] | .name'
```

**Select items based on condition:**
```bash
echo '[1, 5, 3, 0, 7]' | jq 'map(select(. >= 5))'
# Output: [5, 7]
```

**String interpolation:**
```bash
echo '42' | jq '"The input was \(.)"'
```
