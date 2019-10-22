# Creating Starter Application
## Minimal boilerplate
You can create a starter application by using `singlepage create` command. 
```console
$ create myapp
Creating singlepage app in \projects\myapp
Installing packages...
npm notice created a lockfile as package-lock.json. You should commit this file.
added 9 packages from 9 contributors and audited 9 packages in 1.382s
found 0 vulnerabilities

Singlepage starter app created successfully.
```
The command will create the right directory structure and install needed node packages in the application directory. The resulting 
directory structure will look like the one shown below.
```
myapp
  |-assets
    |-favicon.ico
    |-images
      |-app_logo.png
      |-avatar.png
      |-landing.svg
  |-config.json
  |-lib
    |-splib.esm.js
    |-spserver.js
  |-node_modules
  |-package-lock.json
  |-package.json
  |-server
    |-app.json
    |-services
      |-EchoService.js
  |-src
    |-components
      |-Echo.vue
    |-main.js
    |-www
      |-css
        |-bootstrap-grid.css
        |-bootstrap-reboot.css
        |-bootstrap.css
        |-sp.css
      |-index.html
      |service_tester.html
```
Contents of the starter app directories and their intented use is summarized in the table below.
|Directory/File   |Description   |  Modifiable|
|------------|--------------|------------|
|assets      |Everything under assets directory is copied to the client root directory without any changes. You can add files to this directory and refer to them in your components by prefixing it with CDN_URL config option.|Yes|
|assets/app_logo.png|Logo displayed on the splash screen and top left corner on the app when it is loaded. You can replace this file with your own logo|Yes
|assets/images/avatar.png|Default avatar image|Yes
|assets/images/landing.svg|SVG image used in the starter app. You can delete this image if you change the display of splash screen component.|Yes|
|config.json|App configuration. See the Configuration Parameters sections for a description of available configuration parameters.|Yes|
|lib|Contains Singlepage server and client libraries.Your code will reference the files in these directories. Do not alter these files.|No|
|server/app.json|Application definition file. This file will get modified when you edit your application via Singlepage admin UI. We recommend not manually editing this file unless you really know what you are doing.|No
|server/services|Directory where you will put your *Service.js files. These files will be automatically registered in Singlepage service registry with the same name as the file name minus the extension. `EchoService.js` is a sample service that illustrates basic service structure.|Yes|
|src/components|Directory for application Vue.js components. A sample component Echo.vue is provided as an example. You can add more .vue files to this directory for your components. The components will be registered with the same name as the file name minus the .vue extension.|Yes|
|src/main.js| The entry file for rollup.js bundle for your application.|Yes|
|src/www/css/bootstrap*.css|Files for themeing your application. We recommend not editing bootstrap and grid files.|Yes|
|src/www/css/sp.css|Core Singlepage styles that generally constant across look&feel.|Yes|
|src/www/index.html|Index file template. You can modify this file but do not edit the mustache variables.|Yes|
|src/www/service_tester.html|Simple interface to test Singlepage services|No|

## Creating Boilerplate with Full Customization
Use `-f` or `--full` flag to create additional customization files.
```console
$ singlepage create myapp -f
```
This option will write a few more files that offer customization of Singlepage applications. The additional or modified files written in the full mode are summarized below.
|Directory/File   |Description   |
|------------|--------------|
|src/locales/messages_en-US.json|Messages file for internationalization. Strings defined in this file will override default messages for `en-US` locale. If your locale is set differently, create a file named messages_<locale>.json. For example, if LOCALE is set to `fr` in config.json, define your messages in messages_fr.json.|
|src/templates/component_templates.json|Defines new CSS styles for existing component windows and allows overriding default display styles.|
|src/templates/page_four_equal_columns.xml|An example page layout grid. You can create your own page layouts by defining XML files that start with page_.|
|src/main.js|Modified main.js files that passes more customization options to application initialization method.|
|src/App.vue|The main singlepage Vue component. Edit this only if know what you are doing|
|src/Login.vue|Vue component that shows login page|
|src/Logout.vue|Vue component that displays after a user logs out|
|src/PageNotFound.vue|Component displayed when a page is not found|


