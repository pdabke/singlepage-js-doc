# Application Development
`singlepage-js` offers a `serve` command that starts a Web server and builds your application in memory and serves it. The `serve` mode watches your component
and services files as well as HTML/CSS source and reloads browser after compiling changed files.
```
$ singlepage serve --help
Usage: serve [options]

Options:
  -p, --port <port>          HTTP port
  -P, --https-port <port>    HTTPS port
  -c, --cert <cert-file>     HTTPS cert file
  -k, --key <key-file>       HTTPS key file
  -a, --app-base <app-base>  Appliction root directory.
  -h, --help                 output usage information

$ cd myapp

$ singlepage serve
Building app components...
Running in watch mode
Registered /projects/myapp/server/services/EchoService.js as EchoService
Starting http server on port 8080

```

Developing an application on `singlepage-js` consists of the following major tasks:
- Customizing application look & feel
- Developing Web services
- Developing Vue.js components
Details of each of these areas of development are explained in the next few sections of the documentation.

