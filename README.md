MDiMapGeocoder
===============

A library to use [Maryland's cascading geocoder](http://geodata.md.gov/imap/rest/services/GeocodeServices/MD_CompositeLocatorWithZIPCodeCentroids/GeocodeServer) in Node.js and the browser

[![NPM](https://nodei.co/npm/mdimapgeocoder.png?global=true)](https://nodei.co/npm/mdimapgeocoder/)

##Installation

###Node.js

* Run `npm install mdimapgeocoder`

```javascript
var MDiMapGeocoder = require('mdimapgeocoder')
```

###Browser
* Download build/MDiMapGeocoder.min.js

```html
<script src="MDiMapGeocoder.min.js"></script>
```

##Usage

```javascript
MDiMapGeocoder.search(address, options?, callback)
```

- **address** - string containing full address or object containing Street, City, State, ZIP
- **options** - optional object containing search options (see below)
- **callback** - function(error, response) {}

### Example
```javascript

//Single Line
MDiMapGeocoder.search('1101 Camden Ave, Salisbury MD 21801', function(err, res){
  // example response
  res.candidates[0] = 
    {
      "address" : "1101 CAMDEN AVE, SALISBURY, MD, 21801",
      "location" : {
        "x" : -75.609389996999937,
        "y" : 38.342533962000061
      },
      "score" : 100,
      "attributes" : {}
    }
})

//Address Fields
MDiMapGeocoder.search({
  Street: '1101 Camden Ave',
  City: 'Salisbury',
  State: 'MD',
  ZIP: '21801'
}, function(err, res){
  
})
```

### Options
- **wkid** (integer) - Specify WKID to return. Default 4326

```javascript
var address = '1101 Camden Ave, Salisbury MD 21801'
var options = {wkid: 26985} // MD State Plane
MDiMapGeocoder.search(address, options, function(err, response) {
  // response.location = {"x":521564.8398928333,"y":75950.13939312194}
})
```

- **outFields** (array) - The list of fields to be included in the returned results. You may specify any candidate field from the service resource.

```javascript
var address = '1101 Camden Ave, Salisbury MD 21801'
var options = {outFields: ['ZIP', 'City']}
MDiMapGeocoder.search(address, options, function(err, response) {
  // response.attributes = { ZIP: '21801', City: 'SALISBURY' } }
})
```