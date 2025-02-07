# Custom HTTP Header

## POST `http://${host}/axis-cgi/customhttpheader.cgi`

* Typically used when encountering CORS issues, you can adjust the headers to resolve them.
* The variable ${host} corresponds to the IP address of your AXIS camera.
* The request method is always executed using POST. To achieve different objectives, simply specify the desired method value (e.g., list, set or remove) in the request body.
* AXIS offers two main types of authentication: Digest Authentication and Basic Authentication. The header settings will depend on the authentication method you choose..

<br/>

<span style="color:rgb(58, 231, 58);">Info:</span> Basic Authentication is only supported for HTTPS connections, while Digest Authentication supports both HTTP and HTTPS when using AXIS OS version 12.1.X or above. For more information check [AXIS OS Release Notes](https://help.axis.com/en-us/axis-os-release-notes).

<span style="color: #ffcc00;">Warning:</span> When performing an AXIS OS upgrade, proceed with caution as your custom header settings will be reset to their default state.

<br/>


## List custom headers

POST `http://${host}/axis-cgi/customhttpheader.cgi`

Request body

```json
{
	"apiVersion": "1.0",
	"method": "list"
}
```

Response

```json
{
    "apiVersion": "1.0",
    "method": "list",
    "data": {
        "X-Content-Type-Options": "nosniff",
        "X-Frame-Options": "SAMEORIGIN",
        "X-XSS-Protection": "1; mode=block",
        "Content-Security-Policy": "default-src 'self'; frame-ancestors 'self'; connect-src 'self' https://*.google-analytics.com https://*.analytics.google.com https://*.googletagmanager.com https://*.axis.com mediastream: blob:; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://*.googletagmanager.com https://www.google-analytics.com https://ssl.google-analytics.com https://*.axis.com; style-src 'self' 'unsafe-inline'; img-src 'self' https://*.google-analytics.com https://*.googletagmanager.com https://*.axis.com data: blob:; media-src 'self' mediastream: blob:; object-src 'none'",
        "Referrer-Policy": "strict-origin-when-cross-origin",
        "Access-Control-Allow-Origin": "http://192.168.1.221"
    }
}
```

<br/>

## Add a custom header

Request body

```json
{
  "apiVersion": "1.0",
  "context": "OptionalContext",
  "method": "set",
  "params": {
    "Access-Control-Allow-Origin": "http://192.168.1.221" //depend on your host
  }
}
```

Response
```json
{
          "apiVersion": "1.0",
          "context": "OptionalContext",
          "method": "set",
          "data": {
            "Access-Control-Allow-Origin": "http://192.168.1.221"
          }
}
```

<br/>

* OS v11.11.116 of AXIS camera existing two authentication methods: Digest Auth and Base Auth. If you choose Digest Auth, the following setting is used for handling the case.

    * Request body
    ```json
    {
    "apiVersion": "1.0",
    "context": "OptionalContext",
    "method": "set",
    "params": {
        "Access-Control-Allow-Origin": "http://192.168.1.221", //depend on your host
        "Access-Control-Expose-Headers": "WWW-Authenticate",
        "Access-Control-Allow-Headers": "Authorization"
    }
    }
    ```

<br/>

## Remove a custom header
```json
{
  "apiVersion": "1.0",
  "context": "OptionalContext",
  "method": "remove",
  "params": {
    "Access-Control-Allow-Origin": "http://192.168.1.221" //depend on your host
  }
}
```

<br/>

## Reference
[Custom HTTP header API - AXIS](https://developer.axis.com/vapix/network-video/custom-http-header-api)
