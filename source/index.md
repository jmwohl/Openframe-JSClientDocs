---
title: Geocodio API Reference

language_tabs:
  - shell
  - ruby
  - python
  - php
  - javascript: Node.js
  - clojure

toc_footers:
 - <a href="https://dash.geocod.io">Sign Up for an API Key</a>
 - <a href="http://geocod.io/terms-of-use/">Terms of Use</a>
---

# Introduction

Geocodio is a geocoding service that aims to fill a void in the community by allowing developers to geocode large amounts of US addresses without worrying about daily limits and high costs.

Our pricing structure is simple, you get the first 2,500 queries per day for free and after that you are charged $0.001 per query (yep, that's $1 per 1,000 geocoding queries).

We provide a simple RESTful API, with a base url at `http://api.geocod.io/v1/`.

<aside class="notice">
Note the versioning prefix in the base url, which is required for all requests.
</aside>

# Libraries

Thanks to the great community we have language bindings for Ruby, Python, PHP, Perl, Node.js and Clojure.

Basic examples for various languages are provided here, but please make sure to check out the full documentation for the individual libraries, linked below.

<table class="table">
  <tbody><tr>
    <th>Platform</th>
    <th>Library</th>
    <th>Featured in documentation</th>
  </tr>
  <tr>
    <td><strong>PHP</strong></td>
    <td><a href="https://github.com/davidstanley01/geocodio-php" target="_blank">davidstanley01/geocodio-php</a> by <a href="https://twitter.com/davidstanley01" target="_blank">@davidstanley01</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><strong>Ruby</strong></td>
    <td><a href="https://github.com/alexreisner/geocoder" target="_blank">alexreisner/geocoder</a> supports Geocodio thanks to PR by <a href="https://twitter.com/dblockdotorg" target="_blank">@dblockdotorg</a></td>
    <td><i class="fa fa-minus"></i></td>
  </tr>
  <tr>
    <td><strong>Ruby</strong></td>
    <td><a href="https://github.com/davidcelis/geocodio" target="_blank">davidcelis/geocodio</a> by <a href="https://twitter.com/davidcelis" target="_blank">@davidcelis</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><strong>Python</strong></td>
    <td><a href="https://github.com/bennylope/pygeocodio" target="_blank">bennylope/pygeocodio</a> by <a href="https://twitter.com/bennylope" target="_blank">@bennylope</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><strong>Python</strong></td>
    <td><a href="https://github.com/davidstanley01/Geocodio.py" target="_blank">davidstanley01/Geocodio.py</a> by <a href="https://twitter.com/davidstanley01" target="_blank">@davidstanley01</a></td>
    <td><i class="fa fa-minus"></i></td>
  </tr>
  <tr>
    <td><strong>Node.js</strong></td>
    <td><a href="https://github.com/desmondmorris/node-geocodio" target="_blank">desmondmorris/node-geocodio</a> by <a href="https://twitter.com/desmondmorris" target="_blank">@desmondmorris</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><strong>Clojure</strong></td>
    <td><a href="https://github.com/jboverfelt/rodeo" target="_blank">jboverfelt/rodeo</a> by <a href="https://twitter.com/j_felt08" target="_blank">@j_felt08</a></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><strong>Perl</strong></td>
    <td><a href="https://github.com/mrallen1/WebService-Geocodio" target="_blank">mrallen1/WebService-Geocodio</a> by <a href="https://twitter.com/bytemeorg" target="_blank">@bytemeorg</a></td>
    <td><i class="fa fa-minus"></i></td>
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

All requests require an API key, you can [register here](https://dash.geocod.io) to get your own API key.

The API key must be included in all requests using the `?api_key=YOUR_API_KEY` query parameter.

Each account can have multiple API keys. This is ideal if you're working on several projects and want to be able to revoke access using the API key for a single project in the future or if you want to keep track of usage per API key.

<aside class="warning">
Make sure to replace `YOUR_API_KEY` with your personal API key found in the [Geocodio dashboard](https://dash.gecod.io).
</aside>

# Geocoding

Geocoding (also known as forward geocoding) allows you to convert one or more addresses into geographic coordinates (i.e. latitude and longitude).

Geocodio supports geocoding of addresses, cities and zip codes in all kinds of various formats.

<aside class="notice">
Make sure to check the [address formats](#toc_21) section for more information on the different address formats supported.
</aside>

You can either geocode a single address at the time or collect multiple addresses in batches in order to geocode up to 10,000 addresses at the time.

## Geocoding single address

A single address can be geocoded by making a simple `GET` request to the *geocode* endpoint, you can <a href="http://api.geocod.io/v1/geocode?q=42370+Bob+Hope+Drive%2c+Rancho+Mirage+CA&api_key=YOUR_API_KEY" target="_blank">try this in your browser right now</a>.

> To geocode a single address:

```shell
curl "http://api.geocod.io/v1/geocode?q=42370+Bob+Hope+Drive%2c+Rancho+Mirage+CA&api_key=YOUR_API_KEY"
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')

location = geocodio.geocode('42370 Bob Hope Drive, Rancho Mirage CA')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)

location = client.geocode("42370 Bob Hope Drive, Rancho Mirage CA")
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');

$location = $client->get('42370 Bob Hope Drive, Rancho Mirage CA');
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);

geocodio.geocode('42370 Bob Hope Drive, Rancho Mirage CA', function(err, location){
    if (err) throw err;

    console.log(location);
});
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable

(single "42370 Bob Hope Drive, Rancho Mirage CA")
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

locations = geocodio.geocode('42370 Bob Hope Drive, Rancho Mirage CA', '1290 Northbrook Court Mall, Northbrook IL', '4410 S Highway 17 92, Casselberry FL', '15000 NE 24th Street, Redmond WA', '17015 Walnut Grove Drive, Morgan Hill CA')

```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)

locations = geocodio.geocode([
  '42370 Bob Hope Drive, Rancho Mirage CA',
  '1290 Northbrook Court Mall, Northbrook IL',
  '4410 S Highway 17 92, Casselberry FL',
  '15000 NE 24th Street, Redmond WA',
  '17015 Walnut Grove Drive, Morgan Hill CA'
])
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');

$data = array(
  '42370 Bob Hope Drive, Rancho Mirage CA',
  '1290 Northbrook Court Mall, Northbrook IL',
  '4410 S Highway 17 92, Casselberry FL',
  '15000 NE 24th Street, Redmond WA',
  '17015 Walnut Grove Drive, Morgan Hill CA'
);
$locations = $client->post($data);
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);

var addresses = [
  '42370 Bob Hope Drive, Rancho Mirage CA',
  '1290 Northbrook Court Mall, Northbrook IL',
  '4410 S Highway 17 92, Casselberry FL',
  '15000 NE 24th Street, Redmond WA',
  '17015 Walnut Grove Drive, Morgan Hill CA'
];

geocodio.geocode(addresses, function(err, locations) {
    if (err) throw err;

    console.log(locations);
});
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable

(batch ["42370 Bob Hope Drive, Rancho Mirage CA", "1290 Northbrook Court Mall, Northbrook IL", "4410 S Highway 17 92, Casselberry FL", "15000 NE 24th Street, Redmond WA", "17015 Walnut Grove Drive, Morgan Hill CA"])
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

If you have several addresses that you need to geocode, batch geocoding is a much faster options since it removes the overhead of having to perform multiple `HTTP` requests.

Batch geocoding requests are performed by making a `POST` request to the *geocode* endpoint, suppliying a `JSON` array in the body.

<aside class="warning">
You can batch geocode up to 10,000 addresses at the time.
</aside>

### HTTP Request

`POST http://api.geocod.io/v1/geocode`

### URL Parameters

Parameter | Description
--------- | -----------
api_key | Your Geocodio API key

# Reverse Geocoding

Reverse geocoding is the process of turning geographic coordinates (i.e. latitude and longitude) into a human-readable address.

Geocodio will find matching street(s) and determine the correct house number based on the location, note that Geocodio doesn't guarantee that the exact house number is valid.

As with forward geocoding, you can either geocode a single set of coordinates at the time or collect multiple coordinates in batches and reverse geocode up to 10,000 coordinates at the time.

This endpoint can return up to 5 possible matches ranked and ordered by an [accuracy score](#toc_20).

<aside class="success">
A geographic coordinate consists of latitude followed by latitude separated by a comma, e.g. `38.9002898,-76.9990361`
</aside>

## Reverse geocoding single coordinate

> To reverse geocode a single coordinate:

```shell
curl "http://api.geocod.io/v1/reverse?q=38.9002898,-76.9990361&api_key=YOUR_API_KEY"
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')

addresses = geocodio.reverse_geocode('38.9002898,-76.9990361')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)

addresses = client.reverse((38.9002898, -76.9990361))
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');

$addresses = $client->reverse('38.9002898,-76.9990361');
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);

geocodio.reverse('38.9002898,-76.9990361', function(err, addresses) {
    if (err) throw err;

    console.log(addresses);
});

```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable

(single-reverse "38.9002898,-76.9990361")
```

> Example response:

```json
{
  "results": [
    {
      "address_components": {
        "number": "500",
        "street": "H",
        "suffix": "St",
        "postdirectional": "NE",
        "city": "Washington",
        "state": "DC",
        "zip": "20002"
      },
      "formatted_address": "500 H St NE, Washington, DC 20002",
      "location": {
        "lat": 38.900203,
        "lng": -76.999507
      },
      "accuracy": 1
    },
    {
      "address_components": {
        "number": "474",
        "street": "H",
        "suffix": "St",
        "postdirectional": "NE",
        "city": "Washington",
        "state": "DC",
        "zip": "20002"
      },
      "formatted_address": "474 H St NE, Washington, DC 20002",
      "location": {
        "lat": 38.900205,
        "lng": -76.99994
      },
      "accuracy": 0.18
    },
    {
      "address_components": {
        "number": "749",
        "street": "5th",
        "suffix": "St",
        "postdirectional": "NE",
        "city": "Washington",
        "state": "DC",
        "zip": "20002"
      },
      "formatted_address": "749 5th St NE, Washington, DC 20002",
      "location": {
        "lat": 38.898911,
        "lng": -76.999509
      },
      "accuracy": 0.18
    }
  ]
}
```

A single coordinate can be reverse geocoded by making a simple `GET` request to the *reverse* endpoint, you can <a href="http://api.geocod.io/v1/reverse?q=38.9002898,-76.9990361&api_key=YOUR_API_KEY" target="_blank">try this in your browser right now</a>.

### HTTP Request

`GET http://api.geocod.io/v1/reverse`

### URL Parameters

Parameter | Description
--------- | -----------
q | The query (i.e. latitude/longitude pair) to geocode
api_key | Your Geocodio API key

## Batch reverse geocoding

> To perform batch reverse geocoding:

```shell
curl -X POST \
  -H "Content-Type: application/json" \
  -d '["35.9746000,-77.9658000","32.8793700,-96.6303900","33.8337100,-117.8362320","35.4171240,-80.6784760"]' \
  http://api.geocod.io/v1/reverse?api_key=YOUR_API_KEY
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')

address_sets = geocodio.reverse_geocode('35.9746000,-77.9658000', '32.8793700,-96.6303900', '33.8337100,-117.8362320', '35.4171240,-80.6784760')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)

address_sets = client.reverse([
  ('35.9746000,-77.9658000'),
  ('32.8793700,-96.6303900'),
  ('33.8337100,-117.8362320'),
  ('35.4171240,-80.6784760)'
])
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');

$address_sets = $client->reverse(array('35.9746000,-77.9658000', '32.8793700,-96.6303900', '33.8337100,-117.8362320', '35.4171240,-80.6784760'));
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);

var coordinates = [
  '35.9746000,-77.9658000',
  '32.8793700,96.6303900',
  '33.8337100,117.8362320',
  '35.4171240,-80.6784760'
];

geocodio.reverse(coordinates, function(err, address_sets){
    if (err) throw err;

    console.log(address_sets);
});
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable

(batch-reverse ["35.9746000,-77.9658000", "32.8793700,-96.6303900", "33.8337100,-117.8362320", "35.4171240,-80.6784760"])
```

> Example response:

```json
{
  "results": [
    {
      "query": "35.9746000,-77.9658000",
      "response": {
        "results": [
          {
            "address_components": {
              "number": "125",
              "predirectional": "S",
              "street": "Alston",
              "suffix": "St",
              "city": "Taylor Crossroads",
              "state": "NC",
              "zip": "27856"
            },
            "formatted_address": "125 S Alston St, Taylor Crossroads, NC 27856",
            "location": {
              "lat": 35.974263,
              "lng": -77.965823
            },
            "accuracy": 1
          },
          {
            "address_components": {
              "number": "126",
              "predirectional": "E",
              "street": "Washington",
              "suffix": "St",
              "city": "Taylor Crossroads",
              "state": "NC",
              "zip": "27856"
            },
            "formatted_address": "126 E Washington St, Taylor Crossroads, NC 27856",
            "location": {
              "lat": 35.974456,
              "lng": -77.965429
            },
            "accuracy": 1
          }
        ]
      }
    },
    {
      "query": "32.8793700,-96.6303900",
      "response": {
        "results": [
          {
            "address_components": {
              "number": "100",
              "predirectional": "E",
              "street": "Kingsley",
              "suffix": "Rd",
              "city": "Centerville",
              "state": "TX",
              "zip": "75041"
            },
            "formatted_address": "100 E Kingsley Rd, Centerville, TX 75041",
            "location": {
              "lat": 32.878693,
              "lng": -96.630918
            },
            "accuracy": 1
          },
          {
            "address_components": {
              "number": "2961",
              "predirectional": "S",
              "street": "1st",
              "suffix": "St",
              "city": "Centerville",
              "state": "TX",
              "zip": "75041"
            },
            "formatted_address": "2961 S 1st St, Centerville, TX 75041",
            "location": {
              "lat": 32.881541,
              "lng": -96.630962
            },
            "accuracy": 0.92
          },
          {
            "address_components": {
              "number": "3084",
              "predirectional": "S",
              "street": "1st",
              "suffix": "St",
              "city": "Centerville",
              "state": "TX",
              "zip": "75041"
            },
            "formatted_address": "3084 S 1st St, Centerville, TX 75041",
            "location": {
              "lat": 32.878897,
              "lng": -96.630992
            },
            "accuracy": 0.87
          }
        ]
      }
    },
    {
      "query": "33.8337100,-117.8362320",
      "response": {
        "results": [
          {
            "address_components": {
              "number": "2700",
              "predirectional": "N",
              "street": "Tustin",
              "suffix": "St",
              "city": "O`range`",
              "state": "CA",
              "zip": "92865"
            },
            "formatted_address": "2700 N Tustin St, O`range`, CA 92865",
            "location": {
              "lat": 33.832923,
              "lng": -117.836211
            },
            "accuracy": 1
          }
        ]
      }
    },
    {
      "query": "35.4171240,-80.6784760",
      "response": {
        "results": []
      }
    }
  ]
}
```

If you have several coordinates that you need to reverse geocode, batch reverse geocoding is a much faster options since it removes the overhead of having to perform multiple `HTTP` requests.

Batch reverse geocoding requests are performed by making a `POST` request to the *reverse* endpoint, suppliying a `JSON` array in the body.

<aside class="warning">
You can batch reverse geocode up to 10,000 coordinates at the time.
</aside>

### HTTP Request

`POST http://api.geocod.io/v1/reverse`

### URL Parameters

Parameter | Description
--------- | -----------
api_key | Your Geocodio API key

# Addres parsing

If you just need to an address into individual components, Geocodio can help you too. 

<aside class="notice">
Note: Address parsing is free of charge and does not count towards your API usage, you will however still need an API key.
</aside>

> To parse an address:

```shell
curl "http://api.geocod.io/v1/parse?q=42370+Bob+Hope+Drive%2c+Rancho+Mirage+CA&api_key=YOUR_API_KEY"
```

```ruby
require 'geocodio'

geocodio = Geocodio::Client.new('YOUR_API_KEY')

address = geocodio.parse('42370 Bob Hope Drive, Rancho Mirage CA')
```

```python
from geocodio import GeocodioClient

client = GeocodioClient(YOUR_API_KEY)

address = client.parse('42370 Bob Hope Drive, Rancho Mirage CA')
```

```php
<?php
require_once 'vendor/autoload.php'
use Stanley\Geocodio\Client;

// Create the new Client object by passing in your api key
$client = new Client('YOUR_API_KEY');

$address = $client->parse('42370 Bob Hope Drive, Rancho Mirage CA');
```

```javascript
var Geocodio = require('geocodio');

var config = {
    api_key: 'YOUR_API_KEY'
}

var geocodio = new Geocodio(config);

geocodio.parse('42370 Bob Hope Drive, Rancho Mirage CA', function(err, address) {
    if (err) throw err;

    console.log(address);
});
```

```clojure
(ns my.ns
  (:require [rodeo.core :refer :all]))

;; You can set the API key in the GEOCODIO_API_KEY environment variable

(components "42370 Bob Hope Dr, Rancho Mirage CA")
```

> Example response:

```json
{
  "address_components": {
    "number": "42370",
    "street": "Bob Hope",
    "suffix": "Dr",
    "city": "Rancho Mirage",
    "state": "CA"
  },
  "formatted_address": "42370 Bob Hope Dr, Rancho Mirage CA"
}
```

### HTTP Request

`GET http://api.geocod.io/v1/parse`

### URL Parameters

Parameter | Description
--------- | -----------
q | The query (i.e. address) to parse
api_key | Your Geocodio API key

<aside class="notice">
Make sure to check the [address formatting](#toc_20) section for more information on the different address formats supported.
</aside>

# Accuracy score
Each geocoded result is returned with an accuracy score, a decimal number ranging from 0.00 to 1.00. This score is generated by the internal Geocodio engine based on how accurate the result is believed to be. The higher the score the better the result.

For example, if against all odds an address simply can't be found — instead of returning no results, Geocodio will return a geocoded point based on the zip code or city but with a much lower accuracy score.

Results are always returned ordered by accuracy score.

# Address formats
Geocodio allows you to geocode addresses, cities or zip codes. A street addresses needs to have either a zip or a city/state combination included. If a city is provided without a state, Geocodio will automatically guess and add the state based on what it most likely might be.

Addresses that are used with the Geocoding API need to be predictably formatted, here are some examples of valid addresses:

* 42370 Bob Hope Dr, Rancho Mirage CA
* 42370 Bob Hope Drive, Rancho Mirage CA
* 42370 Bob Hope Dr, Rancho Mirage, CA
* 42370 Bob Hope Dr, Rancho Mirage CA
* 42370 Bob Hope Dr, 92270
* Rancho Mirage, CA
* Rancho Mirage
* 92270

# Errors
> Here is an example of a 422 Unprocessable Entity response:

```json
{
  "error": "Could not geocode address, zip code or city/state are required"
}
```

The Geocodio API employs semantic HTTP status codes. This is some of the status codes you can expect to see:

Error Code | Meaning
---------- | -------
200 OK | Hopefully you will see this most of the time. Note that this status code will also be returned even though no geocoding results were available
403 Forbidden | Invalid API key or other reason why access is forbidden
422 Unprocessable Entity | A client error prevented the request from executing succesfully (e.g. invalid address provided). A JSON object will be returned with an error key containing a full error message
500 Server Error | Hopefully you will never see this...it means that something went wrong in our end. Whoops.


# Client-side access
> To Geocode an address using a jQuery AJAX call.

```html
<script>
var address = '42370 Bob Hope Dr, Rancho Mirage CA',
    apiKey = 'YOUR_API_KEY';

$.get('http://api.geocod.io/v1/geocode?q='+ encodeURIComponent(address) +'&api_key=' + encodeURIComponent(apiKey), function (response) {
  console.log(response.results);
});
</script>
```

The Geocodio API supports `CORS` using the `Access-Control-Allow-Origin` *HTTP* header. This means that you will be able to make requests directly to the API using JavaScript.

See an example to the right.

<aside class="notice">
**Note:** This will expose your API Key publicly, make sure that you understand and accept the implications of this approach.
</aside>

# Contact & Support
Have any questions? Feel free to tweet us [@Geocodio](http://twitter.com/Geocodio) or shoot us an email [support@geocod.io](mailto:support@geocod.io).

