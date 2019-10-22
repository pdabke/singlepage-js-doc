# Overview
`singlepage-js` allows you to build your Web application by assembling a collection of Vue.js components.Each Vue component is defined in its own
file in a format called `Single File Component`. You simply have to place the SFC files for all your components in `src/components` directory of
your application. `singlepage-js` will compile the component code to Javascript and either serve it from memory in the development mode or place 
the compiled JS file in `client/components` directory. Components are loaded in the browser only when they are displayed the first time. The
delayed loading keeps the initial code size small and improves response.

`singlepage-js` does not impose any special requirements on your Vue components but you can optionally choose to utilize additional framework
functionality. Every Vue component registered with `singlepage-js` has access to `$app` object that acts as a gateway to other `singlepage-js` 
objects that expose framework functionality. A listing of these helper objects is given below. Subsequent sections in this documentation provide more details on how to use them.

| Object | Description |
|---------|-------------|
|  constants | Define system constants such as method invocation status codes, role names, etc.| 
|  config | Client-side configuration parameters | 
|  rpc | Enables calling methods on Singlepage services | 
|  modal | Modal dialogs creator | 
|  validator | Provides validation of user inputs | 
|  user | Information about the currently logged-in user | 
