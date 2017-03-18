---
date: 2016-03-09T00:11:02+01:00
title: Configuring beacon
weight: 10
---

Beacon uses **gcfg** (INI-style config files for go structs).

```
[beacon]
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

* **`[beacon]`**  
     `port:`  the port the API listens on.  
     `tokensize:` the length of authorization string returned from the client  
     `tokendictionary:` the allowed characters that make up the client authentication string  

* **`[redis]`**  
   `host:`  this is the ip and port that the redis backend is running on  
   `password:`  password to the redis database- 

* **`[ssl]`**  
   `usessl:`  boolean (takes true/false) weather or not to use ssl. Defaults to no  
   `servercert:`  relative path to ssl cert  
   `serverkey:`  relative path to ssl private key  
