# Implementing Web Service
The best way to understand how to write a Web service is to follow an example. When you create the starter application, it includes a sample service named
`EchoService`. The code for the service is listed below. 

```javascript
"use strict";
var _SP = null;
var _COUNT = 1;

const EchoService = {
  async init(config, SP) {
    _SP = SP;
    if (config.EchoService && config.EchoService.count) _COUNT = config.EchoService.count;
  },
  async echo(params, clientInfo, userInfo, roles) {
    if (!params.words) return new _SP.AppError('error_must_type_words_to_echo');
    var resp = '';
    for (let ii=0; ii<_COUNT; ii++) {
      resp = resp + ' ' + params.words;
    }
    return resp;
  }
}
module.exports = EchoService;
```
## Service Initialization
Any service registered with `singpage-js` can have an optional `init` method. `singlepage-js` will call this method once when the service is registered. 
The config object supplied in the `init` method contains parameters defined in `config.*.json` files as explained in the `Configuration Parameters` section. 
 Your service should either set its initial
state based on the config object or store the value in a local variable so that you can retrieve configuration parameters when you need it in processing
a method call.

The second parameter is a container for holding objects useful for interacting with `singlepage-js` framework. It provides two objects: `AppError` and 
`ServiceDirectory`. Use of `AppError` object is described in the `Error Handling` subsection below. `ServiceDirectory` object provides access to other
services registered with `singlepage` via `getService` and `getInternalService` methods. Simply call these methods with the service name as the only
argument to get the corresponding service object.

## Implementing Service Methods
`EchoService` contains a single method `echo` representing its business logic. Happy path execution of a method simply returns a JSON-serializable object, 
in this case just a string.

 > async is not really required here but we use it here to highlight support for that syntax. When `singlepage-js` calls a service, it uses await allowing you to code with cleaner await/async syntax for asynchronous processing.

All your service methods are called with four parameters:

* params - Parameters object specific to the method. In the example, it is expected to have two attributes: num1, num2

* clientInfo - At present it has only three attributes. siteURL and siteId are the URL and database record id for the Website the request is coming from. If you are using `singlepage-js` to create multiple Websites, this information will help you serve site-specific content. In addition it has a tenantId attribute, this will become useful once multi-tenancy support in `singlepage-js` is fully fleshed out.

* userInfo - If the user is not logged in, this object will be null; otherwise it will have the user meta-data attributes. An example is shown below. Note that displayName is computed from screen name, first name and last name depending on what is available. Also, the profile object will vary depending on the type of information your application is collecting for the user.

* roles - Roles is an array of role names for the current site. Possible role names are: 'OWNER', 'SUPERADMIN', 'ADMIN', 'MODERATOR', 'REVIEWER', 'MEMBER', 'GUEST', 'PLATINUM', 'GOLD', 'SILVER', 'BRONZE'

```json
// clientInfo object for site http://localhost:8080 with site ID 1 and tenant ID 1
{
    "siteURL": "http://localhost:8080",
    "siteId": 1,
    "tenantId": 1
}
​
// Sample userInfo object
{
    "firstName": "Prakash",
    "lastName": "Joshi",
    "email": "prakash_joshi@singlepagejs.com",
    "screenName": "pjoshi",
    "displayName": "pjoshi",
    "userData": {
        "profile": { "gender": "M", "age": 64 }
    }
}
```

> Note that in the simplest one-user mode, the tenant/site/user related information is either hardcoded or not very useful. We show it here for the
sake of completeness and for applications that allow user logins other than the admin user.

## Error Handling

We recommend throwing error in case of missing parameters or other errors that can be attributed to bad programming. `singlepage-js` will catch the error, log it to the console and return Internal error code to the caller. If there is an application error, you need to return an instance of `SP.AppError` object with an error message string. `singlepage-js` will return this information to the caller in the format specified later in this section. Note that you can return a message key as the error string so that it gets internationalized when displayed.

It is also possible to provide structured error information about the parameters. This is very useful when the client is using a form to submit data to your service and you want to convey one or more form fields that may be invalid. In that case construct AppError object with two parameters: the error message and an object that provides more detailed information about the error:

```javascript
return new _SP.AppError('error_please_fix_errors', {words: 'error_must_type_words_to_echo'});
```