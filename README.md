# REST-API

This is A simple PHP web application which converts a location into latitude and longitude using the Google Maps API. Then it uses those coordinates to pull images that ware taken in that location from the Instagram API
This example was built for DevConZm Talk

1. You will need an instagram client iD [Instagram Developer](https://www.instagram.com/developer/)'

```php
if (!empty($_GET['location'])) {
    /**
     * Here we build the url we'll be using to access the google maps api
     */
    $maps_url = 'https://' .
        'maps.googleapis.com/' .
        'maps/api/geocode/json' .
        '?address=' . urlencode($_GET['location']);
    $maps_json = file_get_contents($maps_url);
    $maps_array = json_decode($maps_json, true);
   /**
     * Here your lat and lng will be
     */

    $lat = $maps_array['results'][0]['geometry']['location']['lat'];
    $lng = $maps_array['results'][0]['geometry']['location']['lng'];

    /**
     * how we will make our Instagram api request. We'll build the url using the
     * coordinate values returned by the google maps api
     */
    $url = 'https://' .
        'api.instagram.com/v1/media/search' .
        '?lat=' . $lat .
        '&lng=' . $lng .
        '&client_id=CLIENT-ID'; //replace "CLIENT-ID"

    $json = file_get_contents($url);
    $array = json_decode($json, true);
}
```
Facebook [here](http://facebook.com/cynojine)
