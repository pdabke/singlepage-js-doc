# Component Internationalization
## Portal Internationalization
Singlepage supports internationalization at the portal level as described in the `Internationalization` section. Every component has access to messages defined in the portal localized messages file. This remainder of this section describes defining messages that are specific to your component.

## Localizing Messages in Your Component
If your component wants to localize its content, it needs to specify a messages object in data. The following snippet shows messages object defined as part of data.
```html
<script>
'use strict';
module.exports = {
  data: function() {
    return {
      user: 'Keshav',
      messages: {
        "en-US": {
          "msg_hello_user": "Hello {userName}"
        },
        "fr": {
          "msg_hello_user": "Bonjour {userName}"
      }
      :
      :
</script>
```
> You do not have to include message keys again if it is one of the SinglePage system messages. 

Now that you have defined your translations, you can localize content using $i18n function. The template shown below will display Bonjour Keshav if the portal locale is set to fr.
```html
<template>
    <div class="alert alert-info">
        {{$i18n('msg_hello_user', {userName: user})}}
    </div>
</template>
```
## Passing Messages to Child Components
Sometimes a parent component can contain children that eventually end up displaying localized messages. For example many SinglePage built-in components use `sp-form` component that can display error messages specific to the parent component. In this case you can use messages property on the a sub-component and pass the messages object down to a child as a property. The following code snippet from sp-calculator example included in SinglePage distribution illustrates this method. In this case, the form will display the right english message when the backend service returns `msg_error_denominator_cannot_be_zero` error message.
```html
<template>
    <div class="card-body">
      <div class="alert alert-info">{{result}}</div>
      <sp-form :form-def="calcForm" :data-object="calcInput" :errors="calcErrors" 
          save-label="msg_divide" saver-service="CalculatorService" :save-callback="calcSuccess"
          saver-method="divide" :messages="messages"></sp-form>
    </div>
</template>
<script>
'use strict';
module.exports = {
  mounted: function() {
    this.result = this.$i18n("msg_no_result");
  },
  data: function() {
    return {
      messages: {
        "en-US": {
          "msg_number_1": "Numerator",
          "msg_number_2": "Denominator",
          "msg_divide": "Divide",
          "msg_error_denominator_cannot_be_zero": "Denominator cannot be zero.",
          "msg_result": "Result: {result}",
          "msg_no_result": "Please enter the numbers for division and click Divide button."
        }
      },
      result: '',
```

## Accessing Portal Locale
In general we recommend the method described in this page to localize your content. This does not require you to know the portal locale. However, if you needed the current locale for some reason, it is available as `$app.config.LOCALE`.

