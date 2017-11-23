# /users/me/cars

Get all *cars* from the connected user

## Basics

`[GET] https://cloud.xee.com/v3/users/me/cars`

> You'll need the *cars_read* scope.

Secured by **OAuth 2** access token.

## Request

### Headers

|Header name|Header value|Mandatory|
|---|---|---|
|Authorization|`Bearer` with the *OAuth2* access token|YES|

### Url Parameters

There is no parameter for this API

## Success Response

- Status Code: `200`
- Body:

```javascript 
[
	{
	    "id": 1337,
	    "name": "Mark-42",
	    "make": "Mark",
	    "model": "42",
	    "year": 2014,
	    "numberPlate": "M-42-TS",
	    "deviceId": "E133742015",
	    "cardbId": 210,
	    "creationDate": "2014-09-23T12:49:48+00:00",
	    "lastUpdateDate": "2016-02-19T08:41:58+00:00"
	},
	{
	 	...
	}
]
```

|Property|Type|Comment|
|---|---|---|
|id|integer||
|name|string||
|make|string|Might be `generic`|
|model|string|Might be `null`|
|year|integer|Might be `0`|
|numberPlate|string|Might be `null`|
|deviceId|string|The `serial number` of the device. Might be `null` if the car has no device associated|
|cardbId|integer|Represents the type of the *car* from our point of view, that's how we speak to them|
|creationDate|date||
|lastUpdateDate|date||

## Errors

> See how errors are formed in [v3 Readme](../../README.md)

> Be aware of [authentication errors](../../auth/README.md)

|Reason|Status Code|Type|Message|Tip|
|---|---|---|---|---|
|Scope `cars_read` is missing|`403`|`AUTHORIZATION_ERROR`|Token does not have the required scope|Add the cars_read scope to your app scopes and reconnect the user|