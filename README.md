garage-door-sensor
==================

MQTT based sensor to detect whether the garage door is open

MQTT Topic Layout
-----------------

### Publish

* Get door open/closed status

  ```
  ha-sts/garagedoor/{id}/status
  ```

  Format: Sends a string containing either the word "open" or "closed".

  This endpoint publishes a string containing the word "open" when the sensor detects the
  garage door open or status is refreshed while the door is already open.  This endpoint
  publishes the word "closed" when the sensor detects the garage door close or status is
  refreshed while the door is already closed.

### Subscribe

* Refresh / resend status

  ```
  ha-sts/garagedoor/{id}/refresh
  ha-sts/garagedoor/refresh
  ha-sts/refresh
  ```

  Format: Receives a string containing "true".

  These endpoints wait for the word "true" on the topic, then initiate a refresh cycle.
  The refresh cycle resends the status of the garage door as detected by the sensor.  The
  endpoints without the _id_ value are broadcast-like topics.

* Open / Close door

  ```
  ha-sts/garagedoor/{id}/openclose
  ```

  Format: Receives a string containing "true".

  This endpoint waits for the word "true" on the topic, then triggers the garage door
  opener.  The trigger will be a dry contact (or similar) output to simulate pressing
  the open/close button on the garage door opener.
