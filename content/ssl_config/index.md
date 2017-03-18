---
date: 2016-03-09T00:11:02+01:00
title: SSL Configuration
weight: 10
---

Beacon supports SSL out of the box.  The implementation is pretty simple, but results an 'A' on [Qualys SSL Labs](https://www.ssllabs.com/).  If a more lenient SSL implementation is needed you can edit the tls config portion of beacon.go.  

```
tlsConfig := &tls.Config{
	MinVersion:               tls.VersionTLS12,
	CurvePreferences:         []tls.CurveID{tls.CurveP521, tls.CurveP384, tls.CurveP256},
	PreferServerCipherSuites: true,
	CipherSuites: []uint16{
		tls.TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,
		tls.TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,
		tls.TLS_RSA_WITH_AES_256_CBC_SHA,
	},
	ClientSessionCache: tls.NewLRUClientSessionCache(128),
}
```
A more lenient config would look like this:
```
tlsConfig := &tls.Config{
	MinVersion: tls.VersionTLS12,
	MaxVersion: tls.VersionTLS12,
	CipherSuites: []uint16{
		tls.TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,
		tls.TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA,
		tls.TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,
		tls.TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA,
		tls.TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,
		tls.TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,
		tls.TLS_RSA_WITH_AES_128_CBC_SHA,
		tls.TLS_RSA_WITH_AES_256_CBC_SHA,
		tls.TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA,
		tls.TLS_RSA_WITH_3DES_EDE_CBC_SHA,
	},
	PreferServerCipherSuites: true,
	ClientSessionCache:       tls.NewLRUClientSessionCache(128),
}
```

The way I tend to use beacon is behind a reverse proxy (nginx) which I use to demark SSL, but the internal SSL implementation has been tested and is a very good stand alone SSL client.

If you intend to put beacon behind a reverse proxy simply set `usetls` to `false` in the config file.
