# Service Registration
Simply place a Javascript file with the name following the pattern `*Service.js` in `server/services`
directory under your application folder. `singlepage` picks up all files that follow the naming pattern, registers them, and invokes
`init` method if any initialization is required.
> If `singlepage-js` discovers a service with the same name as one of the built-in services, it will replace the built-in service 
with your service.


