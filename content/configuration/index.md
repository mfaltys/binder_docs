---
date: 2016-03-09T00:11:02+01:00
title: Configuring binder
weight: 10
---

Binder uses **gcfg** (INI-style config files for go structs).

```
[binder]
	port			= 8808
	tokensize		= 25
	tokendictionary 	= "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"
[redis]
	host			= "localhost:6379"
	password		= ""
[ssl]
	usetls			= true
	servercert		= deps/test.crt
	serverkey		= deps/test.key
```

The config uses some pretty sane defaults but the following fields are configurable:  

* **`[binder]`**  
     `port:`  the port the API listens on.  
     `loglevel:` the verbosity of logs, acceptable fields are 'info', 'cluster', 'debug', 'error'.  
     `secdictionary:` the allowed characters that make up the client authenticaiton string.  
     `sectokensize:` the length of the generated security token.  
     `filedirectory:` the directory to save files to.  
     `bootstrap:` bool whether or not to bootstrap the instance. If set to false the user must manually register upon first start.  
     `delay:` the delay before binder attempts to bind to redis. This is useful when deploying in a container at the same time as redis.

* **`[redis]`**  
   `host:`  this is the ip and port that the redis backend is running on  
   `password:`  password to the redis database  
