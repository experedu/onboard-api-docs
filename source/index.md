---
title: OnBoard Announce - API Reference

language_tabs:
  - shell
  - ruby
  - objective-c

---

# Introduction
> The endpoint is `https://api.onboard.app/`

Welcome to the OnBoard Announce API Documentation.

This API documentation page was created with [Slate](http://github.com/tripit/slate).

# Version
The current version is `2014-02-23`.

# Change Log
## 2014-02-23
Initial Release.

# Authentication

```shell
curl https://api.onboard.app/v1/ \
  -u test_bQZ3qspKvo3cJxwd3TOzHFCSZZ:
```
<blockquote>
  <p class="highlight shell">
    curl uses the <code>-u</code> flag to pass basic auth credentials.
    Adding a colon after your API key will prevent it from asking you for a password.
  </p>
</blockquote>
```ruby
require "onboardapi"
OnBoard::API.key = "test_bQZ3qspKvo3cJxwd3TOzHFCSZZ"
```

> Make sure to replace the key in the example with your API key.

Authentication is based on API keys. The key is meant to be secret as it provides many privileges and should therefore not be used in a unsecure client application such as JavaScript.

Authentication to the API occurs via HTTP Basic Auth. Provide your API key as the basic auth username. You do not need to provide a password. The language libraries handle this for you.

# Classes
A class can be a representation of a complete grade (e.g. elementary schools) or a class that meets on specific times throughout the school year or term (e.g. in high school, university). In addition a class can have one or more students or teachers enrolled.

## Class Object
| Attribute    | Description |
--------------:+--------------
__id__         | __integer__
__name__       | __string__
__short_name__ | __string__<br>8 character or less class name. Uses the first 8 characters of the name if not provided.
__teachers__   | __array__, __[User object](#user-object)__<br>List of teachers administrating this class.
__students__   | __array__, __[User object](#user-object)__<br>List of students enrolled in this class.

## Create a new class
Creates a new class.

### HTTP Request
`POST /v1/classes`

### Parameters
| Parameter    | Description |
--------------:+--------------
__name__       | Name of the class
__short_name__ | `optional` 8 character or less class name. Uses the first 8 characters of the name if not provided.
__start_time__ | Time when the class starts. Assumes Mon-Fri.
__duration__   | Duration of the class in minutes.
__schedule__   | Array of hashes: `start_datetime`, and `duration` in minutes. Takes precedence over `start_time` and `duration` if non-empty.

## Update a class
## Delete a class
## List all classes
