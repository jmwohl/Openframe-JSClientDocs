---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python
  - php
  - perl
  - javascript
  - clojure

toc_footers:
 - <a href="https://dash.geocod.io">Sign Up for an API Key</a>
 - <a href="http://geocod.io/terms-of-use/">Terms of Use</a>
---

# Introduction

Geocodio is a geocoding service that aims to fill a void in the community by allowing developers to geocode large amounts of addresses without worrying about daily limits and high costs.

Our pricing structure is simple, you get the first 2,500 queries per day for free and after that you are charged $0.001 per query (yep, that's $1 per 1,000 geocoding queries).

We provide a simple RESTful API, with a base url at `http://api.geocod.io/v1/`, note the versioning prefix which is required for all requests.

# Libraries

Thanks to the great community we have language bindings for Ruby, Python, PHP, Perl, Node.js and Clojure.

<table class="table">
  <tbody><tr>
    <th>Platform</th>
    <th>Library</th>
    <th>Featured in documentation</th>
  </tr>
  <tr>
    <th>PHP</th>
    <td><a href="https://github.com/davidstanley01/geocodio-php" target="_blank">davidstanley01/geocodio-php</a> by <a href="https://twitter.com/davidstanley01" target="_blank">@davidstanley01</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <th>Ruby</th>
    <td><a href="https://github.com/alexreisner/geocoder" target="_blank">alexreisner/geocoder</a> supports Geocodio thanks to PR by <a href="https://twitter.com/dblockdotorg" target="_blank">@dblockdotorg</a></td>
    <td><i class="fa fa-minus"></i></td>
  </tr>
  <tr>
    <th>Ruby</th>
    <td><a href="https://github.com/davidcelis/geocodio" target="_blank">davidcelis/geocodio</a> by <a href="https://twitter.com/davidcelis" target="_blank">@davidcelis</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <th>Python</th>
    <td><a href="https://github.com/bennylope/pygeocodio" target="_blank">bennylope/pygeocodio</a> by <a href="https://twitter.com/bennylope" target="_blank">@bennylope</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <th>Python</th>
    <td><a href="https://github.com/davidstanley01/Geocodio.py" target="_blank">davidstanley01/Geocodio.py</a> by <a href="https://twitter.com/davidstanley01" target="_blank">@davidstanley01</a></td>
    <td><i class="fa fa-minus"></i></td>
  </tr>
  <tr>
    <th>Node.js</th>
    <td><a href="https://github.com/desmondmorris/node-geocodio" target="_blank">desmondmorris/node-geocodio</a> by <a href="https://twitter.com/desmondmorris" target="_blank">@desmondmorris</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <th>Clojure</th>
    <td><a href="https://github.com/jboverfelt/rodeo" target="_blank">jboverfelt/rodeo</a> by <a href="https://twitter.com/j_felt08" target="_blank">@j_felt08</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <th>Perl</th>
    <td><a href="https://github.com/mrallen1/WebService-Geocodio" target="_blank">mrallen1/WebService-Geocodio</a> by <a href="https://twitter.com/bytemeorg" target="_blank">@bytemeorg</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td colspan="3">Are you the author of an awesome library that you would like to get featured here? Just <a href="mailto:hello@geocod.io">let us know</a>!</td>
  </tr>
</tbody></table>

# Authentication

> To initialize and authenticate using the API key:

```shell
# With shell, you can just pass the query parameter with each request
curl "http://api.geocod.io/v1/api_endpoint_here?api_key=YOUR_API_KEY"
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');
```

```perl
use 5.014;
use WebService::Geocodio;
use WebService::Geocodio::Location;

my $geo = WebService::Geocodio->new(
    api_key => 'YOUR_API_KEY'
);
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable
```

> Make sure to replace `YOUR_API_KEY` with your API key.

All requests require an API key, you can [register here](https://dash.geocod.io) to get your own API key.

The API key must be included in all requests using the `?api_key=YOUR_API_KEY` query parameter.

Each account can have multiple API keys. This is ideal if you're working on several projects and want to be able to revoke access using the API key for a single project in the future or if you want to keep track of usage based on API key.

<aside class="notice">
You must replace `YOUR_API_KEY` with your personal API key found in the [Geocodio dashboard](https://dash.gecod.io).
</aside>

# Geocoding

Geocoding (also known as forward geocoding) allows you to convert one or more addresses into geographic coordinates (i.e. latitude and longitude).

You can either geocode a single address at the time or collect multiple addresses in batches in order to geocode up to 10,000 addresses at the time.

## Geocoding single address

> To geocode a single address:

```shell
curl "http://api.geocod.io/v1/geocode?q=42370+Bob+Hope+Drive%2c+Rancho+Mirage+CA&api_key=YOUR_API_KEY"
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');
```

```perl
use 5.014;
use WebService::Geocodio;
use WebService::Geocodio::Location;

my $geo = WebService::Geocodio->new(
    api_key => 'YOUR_API_KEY'
);
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable
```

> Example response:

```json
{
  "input": {
    "address_components": {
      "number": "42370",
      "street": "Bob Hope",
      "suffix": "Dr",
      "city": "Rancho Mirage",
      "state": "CA"
    },
    "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA"
  },
  "results": [
    {
      "address_components": {
        "number": "42370",
        "street": "Bob Hope",
        "suffix": "Dr",
        "city": "Rancho Mirage",
        "state": "CA",
        "zip": "92270"
      },
      "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA, 92270",
      "location": {
        "lat": 33.738987255507,
        "lng": -116.40833849559
      },
      "accuracy": 1
    },
    {
      "address_components": {
        "number": "42370",
        "street": "Bob Hope",
        "suffix": "Dr",
        "city": "Rancho Mirage",
        "state": "CA",
        "zip": "92270"
      },
      "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA, 92270",
      "location": {
        "lat": 33.738980796909,
        "lng": -116.40833917329
      },
      "accuracy": 0.8
    }
  ]
}
```

### HTTP Request

`GET http://api.geocod.io/v1/geocode`

### URL Parameters

Parameter | Description
--------- | -----------
q | The query (i.e. address) to geocode
api_key | Your Geocodio API key

<aside class="notice">
Make sure to check the [address formatting](#toc_20) section for more information on the different address formats supported.
</aside>

## Batch geocoding

> To perform batch geocoding:

```shell
curl -X POST \
  -H "Content-Type: application/json" \
  -d '["42370 Bob Hope Drive, Rancho Mirage CA", "1290 Northbrook Court Mall, Northbrook IL", "4410 S Highway 17 92, Casselberry FL", "15000 NE 24th Street, Redmond WA", "17015 Walnut Grove Drive, Morgan Hill CA"]' \
  http://api.geocod.io/v1/geocode?api_key=YOUR_API_KEY
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');
```

```perl
use 5.014;
use WebService::Geocodio;
use WebService::Geocodio::Location;

my $geo = WebService::Geocodio->new(
    api_key => 'YOUR_API_KEY'
);
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable
```

> Example response:

```json
{
  "results": [
    {
      "query": "42370 Bob Hope Drive, Rancho Mirage CA",
      "response": {
        "input": {
          "address_components": {
            "number": "42370",
            "street": "Bob Hope",
            "suffix": "Dr",
            "city": "Rancho Mirage",
            "state": "CA"
          },
          "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA"
        },
        "results": [
          {
            "address_components": {
              "number": "42370",
              "street": "Bob Hope",
              "suffix": "Dr",
              "city": "Rancho Mirage",
              "state": "CA",
              "zip": "92270"
            },
            "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA, 92270",
            "location": {
              "lat": 33.738987255507,
              "lng": -116.40833849559
            },
            "accuracy": 1
          },
          {
            "address_components": {
              "number": "42370",
              "street": "Bob Hope",
              "suffix": "Dr",
              "city": "Rancho Mirage",
              "state": "CA",
              "zip": "92270"
            },
            "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA, 92270",
            "location": {
              "lat": 33.738980796909,
              "lng": -116.40833917329
            },
            "accuracy": 0.8
          }
        ]
      }
    },
    ...
  ]
}
```

### HTTP Request

`POST http://api.geocod.io/v1/geocode`

### URL Parameters

Parameter | Description
--------- | -----------
api_key | Your Geocodio API key

<aside class="notice">
Make sure to check the [address formatting](#toc_20) section for more information on the different address formats supported.
</aside>







# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

# Errors

The Kittn API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The kitten requested is hidden for administrators only
404 | Not Found -- The specified kitten could not be found
405 | Method Not Allowed -- You tried to access a kitten with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The kitten requested has been removed from our servers
418 | I'm a teapot
429 | Too Many Requests -- You're requesting too many kittens! Slown down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.