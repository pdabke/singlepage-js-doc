# Setting Up HTTPS
## Server Options
singlepage.js server can be configured to run using https protocol. When you configure for https, the server still creates an instance that listens using http but it redirects all requests to the https instance. Start the server using options illustrated below.
```javascript
// Options for starting server using https
var options = {
  httpsOptions: {
    key: fs.readFileSync('../credentials/yourhost.key'),
    cert: fs.readFileSync('../credentials/yourhost.crt'),
  },
  httpPort: 8080,
  httpsPort: 8443
};

// Start server
sp.start(options);
```
Now you should be able to access the server on http://your-server-name:8080 as well as https://your-server-name:8443. Visiting http address will redirect to the https instance. You can remove the port numbers if you use default http (80) and https (443) ports.

## Creating Self-Signed Certificate for localhost
Download openssl binary for your platform. Information about pre-built binaries is available on https://​www.openssl.org/community/binaries.html. Use the following command to generate your cert/key pair. Enter 'localhost' for the 'Common name'.
```console
$ openssl req -x509 -sha256 -nodes -newkey rsa:2048 -days 365 -keyout localhost.key -out localhost.crt
```
Running openssl as shown above will create two files: localhost.crt and localhost.key. Copy them to the desired directory andn use them in supplying the https options to singlepage.js server.

 > You may have to download openssl.cnf file if you simply downloaded the openssl binaries. In that case, download the file in the same directory and add -config .\openssl.cnf to the command line shown above.

> Browsers will give you a warning about not being able to verify/trust the Certificate but they will give you an option to proceed (e.g. for Chrome, click on "Advanced" link and follow instructions to bypass browser warning)