# v3

The third version of Xee API

## Why ?

The `v2` of our API was good in terms of content, but there were some *ugly* things.

- Dates were not the same everywhere
- Errors were not the same everywhere
- Sometimes it was v1, sometimes v2

So we decided to build a `v3` to get a new begining. The goal is to be *simple*, *easy*.

- Dates are `RFC3339`
- Errors look the same everytime

## Authentication

> The authentication is a *special* case.

We can't provide a REST API for *authentication* for a simple reason: *User passwords would be known from every single app*

So the authentication is handled by us, in a web page for now (that might change one day for mobiles).

The process is quite simple, don't be afraid!

> Have a look at [auth readme](auth/README.md) for the auth documentation and the **errors it can throw**

|API|Description|
|---|---|
|[`GET /auth/auth`](auth/auth.md)|For the authentication page|
|[`POST /auth/access_token`](auth/access_token.md)|For the *access token* API|

## API

All the **routes** are bellow `https://cloud.xee.com/v3`.

> Note if you need **sandbox APIs** for testing purpose or starting, you can do it by using `https://sandbox.xee.com/v3` as route host.

### Users

This is the first route of our API, from this, you can get the logged in user data

> [Users API](users/README.md) Get the user information, his *id*, his *last name*, *first name*, even his *cars*.

|API|Description|
|---|---|
|[`GET /users/me`](users/me.md)|Get the connected user|
|[`GET /users/me/cars`](users/me/cars.md)|Get all the cars for the connected user|
|[`GET /users/{userId}`](users/user_id.md)|Get a specific user|
|[`GET /users/{userId}/cars`](users/cars.md)|Get all the cars from a user|
|[`POST /users/{userId}/cars`](users/cars_create.md)|Create a car for this user|

### Cars

This is the second route of our API, from this, you can get all the *raw* car data

> [Cars API](cars/README.md) Get the car data, its *id*, its *locations*, even its *trips*.

|API|Description|
|---|---|
|[`GET /cars/{carId}`](cars/car_id.md)|Get a specific car from its *id*|
|[`GET /cars/{carId}/status`](cars/status.md)|Get car *status*|
|[`GET /cars/{carId}/locations`](cars/locations.md)|Get car *locations* history|
|[`GET /cars/{carId}/locations.geojson`](cars/locations-geojson.md)|Get car *locations* history in a [geojson](http://geojson.org/) format|
|[`GET /cars/{carId}/signals`](cars/signals.md)|Get car *signals* history|
|[`GET /cars/{carId}/trips`](cars/trips.md)|Get car *trips*|
|[`GET /cars/{carId}/stats/mileage`](cars/stats/mileage.md)|Get car *mileage* statistic|
|[`GET /cars/{carId}/stats/usedtime`](cars/stats/usedtime.md)|Get car *used time* statistic|

### Trips

This is the third route of our API, from this, you can get all the *trips related* car data

> [Trips API](trips/README.md) Get the *trip* data, its *id*, its *locations*, ...

|API|Description|
|---|---|
|[`GET /trips/{tripId}`](trips/trip_id.md)|Get a specific *trip* from its *id*|
|[`GET /trips/{tripId}/locations`](trips/locations.md)|Get all locations from a *car* during a specific *trip*|
|[`GET /trips/{tripId}/locations.geojson`](trips/locations-geojson.md)|Get all locations from a *car* during a specific *trip* in a [geojson](http://geojson.org/) format|
|[`GET /trips/{tripId}/signals`](trips/signals.md)|Get all signals from a *car* during a specific *trip*|
|[`GET /trips/{tripId}/stats`](trips/trip_id/stats.md)|Get a specific *trip* statistics|
|[`GET /trips/{tripId}/stats/mileage`](trips/trip_id/stats/mileage.md)|Get a specific *trip* mileage|
|[`GET /trips/{tripId}/stats/usedtime`](trips/trip_id/stats/usedtime.md)|Get a specific *trip* duration|

### Devices

This is the fourth route of our API, from this, you can manage your associated devices.
These routes are quite private, and the required scope to call them is not accessible to all the applications.

> [Devices API](devices/README.md) Associate devices to an given user, to a given car ...

|API|Description|
|---|---|
|[`POST /devices/{deviceId}/associate?carId={carId}`](devices/associate_car.md)|Associate a car to the given device|
|[`POST /devices/{deviceId}/associate?pin={pin}`](devices/associate_user.md)|Associate a user to the given device|
|[`POST /devices/{deviceId}/dissociate`](devices/dissociate.md)|Dissociate the given device from it's car|

## Errors

All the errors we throw are mapped on [HTTP Errors codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

### Body

*Except legacy API*, our **errors body** looks like this:

> For legacy API, the errors are explained in the content of the description

```javascript
[
	{
		"type": "ERROR_TYPE",
		"message": "Message on the error",
		"tip": "How to fix the error"
	}
]
```

### List of types

|Type|Description|
|---|---|
|`AUTHENTICATION_ERROR`|Issue with the `Authorization` Header, see more in [Auth README](auth/README.md)|
|`AUTHORIZATION_ERROR`|Issue with the *rights* to access some resources|
|`PARAMETERS_ERROR`|Issue with the *parameters* given in the *API*|
