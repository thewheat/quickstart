# jq Quickstart

- https://github.com/stedolan/jq/
- https://stedolan.github.io/jq/manual/


## Usage

```
echo '{"foo": {"bar": 1}}' | jq .foo.bar

# Output
{
  "foo": {
    "bar": 1
  }
}
```

```
echo '{"foo": {"bar": 1}}' | jq .foo    

{
  "bar": 1
}

```

```
echo '{"foo": {"bar": 1}}' | jq .foo.bar

1
```

## Example file used in examples

`js.json`

```
[
  {
    "index": 0,
    "title": "Invoking jq",
    "link": "https://stedolan.github.io/jq/manual/#Invokingjq"
  },
  {
    "index": 1,
    "title": "Types and Values",
    "link": "https://stedolan.github.io/jq/manual/#TypesandValues"
  },
  {
    "index": 2,
    "title": "Builtin operators and functions",
    "link": "https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions"
  },
  {
    "index": 3,
    "title": "Conditionals and Comparisons",
    "link": "https://stedolan.github.io/jq/manual/#ConditionalsandComparisons"
  },
  {
    "index": 4,
    "title": "Regular expressions (PCRE)",
    "link": "https://stedolan.github.io/jq/manual/#RegularexpressionsPCRE"
  },
  {
    "index": 5,
    "title": "Advanced features",
    "link": "https://stedolan.github.io/jq/manual/#Advancedfeatures"
  },
  {
    "index": 6,
    "title": "Math",
    "link": "https://stedolan.github.io/jq/manual/#Math"
  },
  {
    "index": 7,
    "title": "I/O",
    "link": "https://stedolan.github.io/jq/manual/#IO"
  },
  {
    "index": 8,
    "title": "Streaming",
    "link": "https://stedolan.github.io/jq/manual/#Streaming"
  },
  {
    "index": 9,
    "title": "Assignment",
    "link": "https://stedolan.github.io/jq/manual/#Assignment"
  },
  {
    "index": 10,
    "title": "Modules",
    "link": "https://stedolan.github.io/jq/manual/#Modules"
  },
  {
    "index": 11,
    "title": "Colors",
    "link": "https://stedolan.github.io/jq/manual/#Colors"
  }
]
```


```
cat jq.json | jq .

[
  {
    "index": 0,
    "title": "Invoking jq",
    "link": "https://stedolan.github.io/jq/manual/#Invokingjq"
  },
  {
    "index": 1,
    "title": "Types and Values",
    "link": "https://stedolan.github.io/jq/manual/#TypesandValues"
  },
  {
    "index": 2,
    "title": "Builtin operators and functions",
    "link": "https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions"
  },
  {
    "index": 3,
    "title": "Conditionals and Comparisons",
    "link": "https://stedolan.github.io/jq/manual/#ConditionalsandComparisons"
  },
  {
    "index": 4,
    "title": "Regular expressions (PCRE)",
    "link": "https://stedolan.github.io/jq/manual/#RegularexpressionsPCRE"
  },
  {
    "index": 5,
    "title": "Advanced features",
    "link": "https://stedolan.github.io/jq/manual/#Advancedfeatures"
  },
  {
    "index": 6,
    "title": "Math",
    "link": "https://stedolan.github.io/jq/manual/#Math"
  },
  {
    "index": 7,
    "title": "I/O",
    "link": "https://stedolan.github.io/jq/manual/#IO"
  },
  {
    "index": 8,
    "title": "Streaming",
    "link": "https://stedolan.github.io/jq/manual/#Streaming"
  },
  {
    "index": 9,
    "title": "Assignment",
    "link": "https://stedolan.github.io/jq/manual/#Assignment"
  },
  {
    "index": 10,
    "title": "Modules",
    "link": "https://stedolan.github.io/jq/manual/#Modules"
  },
  {
    "index": 11,
    "title": "Colors",
    "link": "https://stedolan.github.io/jq/manual/#Colors"
  }
]
```

## Get key value for all items in an array of objects
```
cat jq.json | jq '.[] | .title'
cat jq.json | jq '.[] | .["title"]'

"Invoking jq"
"Types and Values"
"Builtin operators and functions"
"Conditionals and Comparisons"
"Regular expressions (PCRE)"
"Advanced features"
"Math"
"I/O"
"Streaming"
"Assignment"
"Modules"
"Colors"
```

### Select multiple keys using comma
```
cat jq.json | jq '.[] | .index,.title'

0
"Invoking jq"
1
"Types and Values"
2
"Builtin operators and functions"
3
"Conditionals and Comparisons"
4
"Regular expressions (PCRE)"
5
"Advanced features"
6
"Math"
7
"I/O"
8
"Streaming"
9
"Assignment"
10
"Modules"
11
"Colors"
```

### Select array index

```
cat jq.json | jq '.[1]'

{
  "index": 1,
  "title": "Types and Values",
  "link": "https://stedolan.github.io/jq/manual/#TypesandValues"
}
```

```
cat jq.json | jq '.[1:3]'  

[
  {
    "index": 1,
    "title": "Types and Values",
    "link": "https://stedolan.github.io/jq/manual/#TypesandValues"
  },
  {
    "index": 2,
    "title": "Builtin operators and functions",
    "link": "https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions"
  }
]
```

## Making an array

```
cat jq.json | jq '[ .[] | .index ]'

[
  0,
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8,
  9,
  10,
  11
]
```

## Making an object
```
cat jq.json | jq '.[] | { i: .index, title }'

{
  "i": 0,
  "title": "Invoking jq"
}
{
  "i": 1,
  "title": "Types and Values"
}
{
  "i": 2,
  "title": "Builtin operators and functions"
}
{
  "i": 3,
  "title": "Conditionals and Comparisons"
}
{
  "i": 4,
  "title": "Regular expressions (PCRE)"
}
{
  "i": 5,
  "title": "Advanced features"
}
{
  "i": 6,
  "title": "Math"
}
{
  "i": 7,
  "title": "I/O"
}
{
  "i": 8,
  "title": "Streaming"
}
{
  "i": 9,
  "title": "Assignment"
}
{
  "i": 10,
  "title": "Modules"
}
{
  "i": 11,
  "title": "Colors"
}
```


## Filtering

```
cat jq.json | jq '.[] | select(.index < 4)'

{
  "index": 0,
  "title": "Invoking jq",
  "link": "https://stedolan.github.io/jq/manual/#Invokingjq"
}
{
  "index": 1,
  "title": "Types and Values",
  "link": "https://stedolan.github.io/jq/manual/#TypesandValues"
}
{
  "index": 2,
  "title": "Builtin operators and functions",
  "link": "https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions"
}
```

## Deleting keys

```
cat jq.json | jq '.[] | del(.index,.title)'

{
  "link": "https://stedolan.github.io/jq/manual/#Invokingjq"
}
{
  "link": "https://stedolan.github.io/jq/manual/#TypesandValues"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions"
}
{
  "link": "https://stedolan.github.io/jq/manual/#ConditionalsandComparisons"
}
{
  "link": "https://stedolan.github.io/jq/manual/#RegularexpressionsPCRE"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Advancedfeatures"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Math"
}
{
  "link": "https://stedolan.github.io/jq/manual/#IO"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Streaming"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Assignment"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Modules"
}
{
  "link": "https://stedolan.github.io/jq/manual/#Colors"
}
```

## Setting / Updating / Replacing values

```
cat jq.json | jq '.[]
   | select(.index < 3) 
   | .title = "Prefix: " + .title 
   | .index += 11 
   | .link = "a new link"
 '

{
  "index": 11,
  "title": "Prefix: Invoking jq",
  "link": "a new link"
}
{
  "index": 12,
  "title": "Prefix: Types and Values",
  "link": "a new link"
}
{
  "index": 13,
  "title": "Prefix: Builtin operators and functions",
  "link": "a new link"
}
```