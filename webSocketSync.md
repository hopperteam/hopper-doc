# Hopper WebSocketSync (v1)
The `WebSocketSync` is for the synchronization of the front- and the backend. The protocol is based upon 
the `WebSocket`-Protocol and uses `JSON` for data serialization.

## Connection
The connection is established by connecting to the WebSocket-Endpoint at `{HOPPER-URL}/api/v1/ws`. 
The Session-Cookie has to be set in the connection request.

## General Communication
The WebSocket connection is used to send `HopperEvent` objects to the frontend. For every event, a single 
WebSocket message with the event (in `JSON` encoding) is sent.

## Data Types
The [hopper data types](./dataTypes.md) are required for the communication. The WebSocketSync adds one more data type:
### `HopperEvent`
  - `type: string` _see Event Types`_ 
  - `data: any` _depends on type_ 

## Event Types
Currently, these event types are supported:
  - `createNotification`: A notification was created, `data` has type `Notification`
  - `updateNotification`: A notification was updated, `data` has type `Notification`
  - `deleteNotification`: A notification was deleted, `data` has type `string` (the notification's `id`)
  - `createSubscription`: A subscription was created, `data` has type `Subscription`
  - `updateSubscription`: A subscription was updated, `data` has type `Subscription`
  - `deleteSubscription`: A subscription was deleted, `data` has type `string` (the subscription's `id`)
