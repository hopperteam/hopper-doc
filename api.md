# Hopper API (v1)
All requests are relative to the hopper domain of the instance you are using. Most probably `dev.hoppercloud.net` or `app.hoppercloud.net`.

## General
This document contains function calls to the RESTful-API. They are written relative to the API: `{HOST}/api/v1`. Parameters are passed as query parameters for `GET` and `DELETE` queries and as JSON objects in the body for `POST` and `PUT` calls. When a `POST` or `PUT` call only has one parameter, the name of it is omitted and the value of parameter is passed directly.

# Backend - Frontend communication

## Request without a valid session

### `GET /` 
Returns API info.

`{"version": "1.0", "type": "dev"}`

### `POST /login (email: string, password: string)`
### `POST /register (email: string, password: string, firstName: string, lastName: string)`
### `POST /forgetPassword (email: string)`
## User Management
from this point on, any request requires a valid session

### `GET /user`
### `PUT /user (email?: string, password?: string, firstName?: string, lastName?: string)`
### `DELETE /user`

## Notification Management
### `GET /notifications (offset?: number, limit?: number, subscription?: string, includeDone?: boolean)`
### `POST /notifications/done (id: string)` 
### `POST /notifications/undone (id: string)`
### `DELETE /notifications (id: string)`

### `WebSocket /ws`
WebSocket sync, see [webSocketSync.md](./webSocketSync.md)
## App Management
### `GET /subscriptions`
Returns all subscriptions the user is subscribed to.

### `DELETE /subscriptions(id: string)`

### `GET /apps(id: string)`
Returns the specified app information.

# Backend - App Communication

### `POST /app (name: string, baseUrl: string, imageUrl: string, manageUrl: string, cert: string)` 
`cert` is a base64 encoded PEM-RSA Public Key. The private key is for authentication of the app to the backend.

### `PUT /app (id: string, content: string)`  
`content` is a stringified JSON-Object containing the `verify` and `data` attribute which is base64 encoded.   
`data` is a JSON-Object containing the fields that want to be updated. Updatable fields are:
  - `name`
  - `imageUrl`
  - `manageUrl`
  - `contactEmail`
  - `cert` 
  
`verify` is a encrypted, using the private key of the app, sha256 hash of the stringified `data` object.

### `POST /notification (subscriptionId: string, notification: Notification)`
### `PUT /notification (id: string, notification?*: Notification)`
### `DELETE /notification (id: string)`

### `GET /subscribeRequest (id: string, content: string): SubscribeRequest`
### `POST /subscribeRequest (id: string, content: string): string`

## Subscribe Process
Navigate the user to `GET {{HOPPER-URL}}/subscribe (id: number, request: string)`

`request` is a encrypted (with the app's key) and base64-encoded representation of the `SubscribeRequest`-JSON.
