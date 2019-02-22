---
title: shift() function
description: The `shift()` function adds a fixed duration to time columns.
aliases:
  - /v2.0/reference/flux/functions/transformations/shift
menu:
  v2_0_ref:
    name: shift
    parent: built-in-transformations
weight: 401
---

The `shift()` function adds a fixed duration to time columns.
The output table schema is the same as the input table.
If the time is `null`, the time will continue to be `null`.

_**Function type:** Transformation_  
_**Output data type:** Object_

```js
shift(shift: 10h, columns: ["_start", "_stop", "_time"])
```

## Parameters

### shift
The amount of time to add to each time value. The shift may be a negative duration.

_**Data type:** Duration_

### columns
The list of all columns to be shifted. Defaults to `["_start", "_stop", "_time"]`.

_**Data type:** Array of strings_

## Examples

###### Shift forward in time
```js
from(bucket: "telegraf/autogen")
	|> range(start: -5m)
	|> shift(shift: 12h)
```

###### Shift backward in time
```js
from(bucket: "telegraf/autogen")
	|> range(start: -5m)
	|> shift(shift: -12h)
```