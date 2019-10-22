# Calling Web Services
Singlepage provides a `rpc` object that can be used to invoke methods on Singlepage Web services. The `Echo` component
code below illustrates how to call a remote Web service. The `echoMessage` method on the component uses the `rpc` object 
to call `echo` method on `EchoService` service.
```html
<template>
  <div class="p-4 d-flex justify-content-center flex-column">
    <form>
      <p><input name="input" class="form-control" v-model="msg"
      placeholder="Type words to echo back from EchoService"></p>
      <input type="submit" value="Echo" class="btn btn-primary" @click.prevent.stop="echoMessage">
    </form>
    <div v-html="echo" class="p-3 mt-3 border bg-light d-flex align-items-center justify-content-center"></div>
  </div>
</template>
<script>
export default {
  data: function() { return {echo: '', msg: ''}},
  
  methods: {
    echoMessage: function() {
      this.$app.rpc.invoke("EchoService", "echo", {words: this.msg}, this.echoSuccess, this.echoFail)
    },

    echoSuccess: function(resp) {
      this.echo = '<div class="lead text-success">' + resp + '</div>';
    },

    echoFail: function(errorCode, error) {
      this.echo = '<div class="lead text-danger">' + errorCode + ' : ' + error + '</div>';
    }
  }

}
</script>

```
The `invoke` method on `rpc` object takes 5 arguments:
 * service - Name of the service as registered with Singlepage
 * method - Method name
 * params - JSON object that is passed to the service
 * successHandler (optional) - Callback in case of successful invocation
 * appErrorHandler (optional) - Callback when the method invocation returns application level error

 If the method call returns successfully Singlepage will call the successHandler (if provided) with one argument representing the
 return value of the method. The argument value will be the JSON object returned by the service.

 ## Method Return Status Codes
 Singlepage defines several return status codes defined on $app.constants object:
  * RETURN_SUCCESS - Method invocation succeeded
  * RETURN_LOGIN_REQUIRED - The user needs to log in to invoke this method
  * RETURN_APP_ERROR - There was an application level error
  * RETURN_ACCESS_DENIED - The user does not have permission to invoke this method
  * RETURN_INTERNAL_ERROR - Internal error
  * RETURN_NO_CONNECTION - Method invocation failed due to network connection issues
  * RETURN_INVALID_REQUEST - Programming error

# Error Handling
If the user does not provide an error callback, Singlepage will display an error dialog. The message displayed in the
dialog will depend on the status code returned. The message displayed can be internationalized via the messages file
as described in the `Internationalization` section. Additionally, for RETURN_NO_CONNECTION, the dialog box will offer
the option to retry the method.

|Error Status|Error Message|
|------------|-------------|
|RETURN_LOGIN_REQUIRED|error_login_required|
|RETURN_APP_ERROR|Localized error message if returned by the service; error_generic otherwise|
|RETURN_ACCESS_DENIED|error_access_denied|
|RETURN_INTERNAL_ERROR|error_generic|
|RETURN_NO_CONNECTION|error_no_connection|
|RETURN_INVALID_REQUEST|error_generic|

User provided error callback is called with the following arguments:
 * Error status code, 
 * Error message string
 * Error details - a JSON object that can provide more details such as invalid form fields