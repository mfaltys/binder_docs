---
date: 2016-03-09T00:11:02+01:00
title: REST API Endpoints
weight: 10
---

## API

Binder exposes an api for uploading, removing, registering, both public files and secrets.  The following  is the specification for endpoints and their protocols.

## Endpoints

**Register Instance**
----
  Registers user with initial key.  This enpoint can be used in cases where the biner instance is not
  bootstrapped.

* **URL**  
  /register
* **Method**  
  `GET`
* **Sample Call**  
  ```
  curl https://cryo.unixvoid.com/register
  ```
* **Returns**  
  `200` : client sec, an alphanumeric string for authorizing/removing entries  
  `400` : the instance has already been registered/bootstrapped. 


**Upload**
----
  Upload a file for public hosting

* **URL**  
  /upload
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
  `file` : file to upload  
  **Optional:**  
  `filename` : an alternate filename to use (overwrites the files actual name)  
  `path` : path to upload the file to 
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 --form filename=/nginx/nginx-1.11.10-linux-amd64 --form file=@nginx https://cryo.unixvoid.com/upload
  ```
* **Returns**  
  `200` : client sec, an alphanumeric string for authorizing/removing entries  
  `400` : security token not set during upload
  `403` : client authentication failed
  `500` : server error/ could not write to filesystem


**Remove**
----
  Remove a file from public host

* **URL**  
  /remove
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
  `filename` : filename/path to remove
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 --form filename=/nginx/nginx-1.11.10-linux-amd64 https://cryo.unixvoid.com/remove
  ```
* **Returns**  
  `200` : entry successfuly removed  
  `400` : security token not set during upload
  `403` : client authentication failed
  `500` : server error/ could not remove from filesystem


**Rotate**
----
  Rotate security token

* **URL**  
  /rotate
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 https://cryo.unixvoid.com/rotate
  ```
* **Returns**  
  `200` : client sec, an alphanumeric string for authorizing/removing entries  
  `400` : security token not set  
  `403` : client authentication failed  
  `500` : server error/ could not set redis key


**Set Key**
----
  Upload a key/value pair for private hosting

* **URL**  
  /setkey
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
  `key`   : the name of the string to privately store
  `value` : the string that is privately stored
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 --form key=TopSecPass --form value=hunter2 https://cryo.unixvoid.com/setkey
  ```
* **Returns**  
  `200` : request processed successfully  
  `400` : security token not set during upload  
  `403` : client authentication failed

**Set File**
----
  Upload a key/file pair for private hosting

* **URL**  
  /setfile
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
  `key`   : the name of the file to privately store
  `value` : the file that is privately stored
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 --form key=binderGPGkey --form value=@keypair.pem https://cryo.unixvoid.com/setfile
  ```
* **Returns**  
  `200` : request processed successfully  
  `400` : security token not set during upload  
  `403` : client authentication failed


**Get Key**
----
  Get a private key/value pair

* **URL**  
  /getkey
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
  `key`   : the name of the string to privately store
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 --form key=TopSecPass https://cryo.unixvoid.com/getkey
  ```
* **Returns**  
  `200` : request processed successfully : key is returned  
  `400` : security token not set during upload  
  `403` : client authentication failed

**Get File**
----
  Get a private key/file pair

* **URL**  
  /getfile
* **Method**  
  `POST`
* **URL Params**  
  **Required:**  
  `sec`   : alphanumeric secret associated with the binder instance  
  `key`   : the name of the file to privately store
* **Sample Calls**  
  ```
  curl -i --form sec=yQHfXWrUMVDNaHoSkDhRhqG26 --form key=binderGPGkey https://cryo.unixvoid.com/getfile
  ```
* **Returns**  
  `200` : request processed successfully : file is returned  
  `400` : security token not set during upload  
  `403` : client authentication failed
