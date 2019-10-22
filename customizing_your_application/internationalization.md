# Overview
At present SinglePage.js supports a pre-configured locale for given portal instance. The locale is not set based on browser locale or a user preference. The default locale is set to `en-US`. You can override the default locale by defining `LOCALE` parameter in the `config.json` (or `config.production.json` or `config.development.json` file.)

Localized message strings are defined in a
file named `messages_<locale>.json`. The message file defines system message strings as well as some common messages (e.g. msg_ok) that can be used
by user-developed components. You can find the `singlepage-js` message files in directory `lib/client/locale` directory under `singlepage-js` install
directory. You can replace default message strings by creating your own file (e.g. messages_en-US.json) in `src/locales` directory under your application
directory. A sample message file is shown below.
```json
{
  "msg_login": "Sign In",
  "msg_register": "Register",
  "msg_logout": "Sign Out"
}
```
> When you define your own messages, make sure you preserve the message variables enclosed in curly braces.
