---
title: OnBoard Announce - API Reference

language_tabs:
  - shell
  - ruby
  - objective-c

---

# Introduction
> The HTTP endpoint of this API is `https://api.onboard.app/`

Welcome to the OnBoard Announce API Documentation.

## How to read this documentation
A few things to keep in mind when reading this documentation:

* Select your language or SDK to show code examples in that language
* All parameters are required unless explicitly marked as `optional`

## Authors & Credits
* Istvan Pusztai: original draft
* [Slate](http://github.com/tripit/slate): what this documentation is built with

# Version
The current version is `2014-02-28`.

# Change Log
## 2014-02-28
Initial draft.

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

Authentication is based on API keys. The key should be kept secret at all times as it provides unrestricted privileges to the tied account and should therefore not be used in a unsecure client application such as JavaScript or as much as possible not stored in source control.

Authentication to the API occurs via HTTP Basic Auth. Provide your API key as the basic auth username. You do not need to provide a password. If you use a language library such as the iOS SDK, this is handled for you.

# Classes
A class can be a representation of a complete grade (e.g. grade school) or a class that meets on specific times throughout the school year or term (e.g. in high school and university). In addition, a class can have one or more students or teachers enrolled.

## Class Object
### Attributes
| Attribute    | Description                                                  |
--------------:+---------------------------------------------------------------
__id__         | __integer__
__name__       | __string__
__short_name__ | __string__<br>8 character or less class name.
__teachers__   | __array__, __[User object](#user-object)__<br>List of teachers administrating this class.
__students__   | __array__, __[User object](#user-object)__<br>List of students enrolled in this class.
__timeslots__  | __array__, __[Time Slot object](#time-slot-object)__<br>Dates & times this class meets on.

## Create a new class
Creates a new class.

### Parameters
| Parameter               | Description                                       |
-------------------------:+----------------------------------------------------
__name__                  | The name of the class.
__short_name__ `optional` | 8 character or less class name. Uses the first 8 characters of the name if empty.
__teachers__   `optional` | List of user IDs who are administrating this class.
__students__   `optional` | List of user IDs who are going to take this class.
__timeslots__  `optional` | Dates & times this class meets on.

## Update a class
## Delete a class
## List all classes

# Time Slot
## Time Slot Object
### Attributes
| Attribute        | Description |
------------------:+--------------
__id__             | __integer__
__start_datetime__ | __datetime__<br>Start date and time.
__duration__       | __integer__<br>Duration in minutes.

## Add a time slot to a course
```shell
curl https://api.onboard.app/v1/classes/{CLASS_ID}/timeslots \
  -u test_bQZ3qspKvo3cJxwd3TOzHFCSZZ:
  -X POST
  -d start_datetime=2014-03-16T14:55:33Z \
  -d duration=90
```

### Parameters
| Parameter        | Description |
------------------:+--------------
__course_id__      | __integer__<br>The ID of the course.
__start_datetime__ | __string__<br>[ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) formatted start date and time<br>e.g. `2014-03-16T14:55:33Z`
__duration__       | __integer__<br>Duration in minutes.

## Update a time slot for a course
```shell
curl https://api.onboard.app/v1/classes/{CLASS_ID}/timeslots/{TIMESLOT_ID} \
  -u test_bQZ3qspKvo3cJxwd3TOzHFCSZZ:
  -X PATCH
  -d duration=60
```

### Parameters
| Parameter                      | Description |
--------------------------------:+--------------
__course_id__                    | __integer__<br>The ID of the course.
__timeslot_id__ | __integer__<br>The ID of the time slot to update.
__start_datetime__<br>`optional` | __string__<br>[ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) formatted start date and time<br>e.g. `2014-03-16T14:55:33Z`
__duration__      <br>`optional` | __integer__<br>Duration in minutes.

## Delete a time slot for a course
```shell
curl https://api.onboard.app/v1/classes/{CLASS_ID}/timeslots/{TIMESLOT_ID} \
  -u test_bQZ3qspKvo3cJxwd3TOzHFCSZZ:
  -X DELETE
```
### Parameters
| Parameter     | Description |
---------------:+--------------
__course_id__   | __integer__<br>The ID of the course.
__timeslot_id__ | __integer__<br>The ID of the time slot to delete.

# Users
A user is anyone who uses the system. They can be administrators, teachers, students, etc. and each of these roles defines what resources they may access.

Roles are defined per-resource and hence only the full admin role is defined on the user object itself.

## User Object
| Attribute       | Description |
-----------------:+--------------
__id__            | __integer__
__full_name__     | __string__<br>The full name of the user. A combination of first and last name.
__first_name__    | __string__
__last_name__     | __string__
__email__         | __string__
__avatar_url__    | __string__
__profile_url__   | __string__
__site_admin__    | __boolean__<br>Set to true to allow this user unrestricted access to any feature on this account.
__created_at__    | __datetime__
__updated_at__    | __datetime__
