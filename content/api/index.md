---
date: 2016-03-09T00:11:02+01:00
title: REST API Endpoints
weight: 10
---

## API

Beacon exposes an api for provisioning id's, updating ip entries, viewing entries, and deleting id's.  The following  is the specification for endpoints and their protocols.

## Endpoints

**Get Value**
----
  Returns registered keys value

* **URL**  
  /`<beacon_id>`
* **Method**  
  `GET`
* **Sample Call**  
  ```
  curl https://beacon.unixvoid.com/unixvoid
  ```


**Provision an ID**
----
  Registers a new ID(key) to use with beacon

* **URL**  
  /provision
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `id` : the intended id to provision  
* **Sample Call**  
  ```
  curl -d id=unixvoid https://beacon.unixvoid.com/provision
  ```
* **Returns**  
  `200` : client sec, an alphanumeric string for authorizing/removing entries  
  `400` : the client id is already in use  


**Update Value**
----
  Update a value for the indended key

* **URL**  
  /update
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `id`    : the intended id to provision  
  `sec`   : alphanumeric secret associated with registered beacon id  
  `value` : value to be updated  
* **Sample Call**  
  ```
  curl -d id=unixvoid -d sec=yQHfXWrUMVDNaHoSkDhRhqG26 -d value=127.0.0.1 https://beacon.unixvoid.com/update
  ```
* **Returns**  
  `200` : value updated successfully  
  `403` : client auth invalid  
  `400` : the client id does not exist  


**Rotate Security Token**
----
  Rotate the security token associated with a registered ID

* **URL**  
  /rotate
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with registered beacon id  
* **Sample Call**  
  ```
  curl -d id=unixvoid -d sec=yQHfXWrUMVDNaHoSkDhRhqG26 https://beacon.unixvoid.com/rotate
  ```
* **Returns**  
  `200` : new client sec, an alphanumeric string for authorizing/removing entries  
  `403` : client auth invalid  
  `400` : the client id does not exist  


**Unregister ID**
----
  Unregister/Remove a registered beacon ID

* **URL**  
  /remove
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `id`    : the intended id to unregister  
  `sec`   : alphanumeric secret associated with registered beacon id  
* **Sample Call**  
  ```
  curl -d id=unixvoid -d sec=yQHfXWrUMVDNaHoSkDhRhqG26 https://beacon.unixvoid.com/remove
  ```
* **Returns**  
  `200` : id unregistered successfully  
  `403` : client auth invalid  
  `400` : the client id does not exist  
