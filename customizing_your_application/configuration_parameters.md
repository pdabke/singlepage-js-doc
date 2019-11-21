# Configuration Parameters
Portal configuration parameters are specified in config.json file located at the top level of your application directory. You can 
define two additional files: config.production.json and config.development.json. The config.development.json file will be merged
with config.json to create the final configuration settings in the development mode. When you create a production distribution, `singlepage-js`
merges config.json with config.production.json and puts it in the dist directory. The list of common configuration settings and server-side
configuration settings is given in the tables below.

## Common Configuration Parameters
| Name | Default Value | Description | 
|------|-------------|--------------|
|  LOCALE| en-US| Lowercased 2-letter locale identifier, optionally including 2-letter dialect (e.g. US)
|  CDN_URL| /sp-files| Set it to CDN URL when the client files are delivered over a CDN or another server
|  SERVICE_URL| null| Set it to `singlepage-js` server URL. Only needed if client files are delivered by another server or CDN|
|  IS_MULTI_SITE| false| Currently unsupported|
|  IS_MULTI_USER| true| Login button is displayed on top if this flag is set to true. If this is false, the app developer can log in by visiting `<app-url>/#/login` page|
|  IS_SELF_REGISTRATION_ALLOWED| false| Currently unsupported|
|  PASSWORD_REGEX| /^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#\$%\^&\*])(?=.{8,})/| Regex the password must comply with.|
|  LOGIN_PREREQS| ['tou_check'] | Currently unsupported |

## Server Configuration Parameters
Please note that we only list the system configuration parameters along with built-in services. Application-specific services may introduce
additional configuration parameters which should be documented by the service provider.
| Name | Default Value | Description | 
|------|-------------|--------------|
|  SITE_TITLE| SinglePage.js| HTML page title for your site (title tag in HTML) |
|  SITE_DESCR| Web site built using SinglePage.js| description meta-tag in the index.html |
|  SITE_KEYWORDS| SinglePage.js , Vue.js| keywords meta-tag in index.html|
|  SITE_AUTHOR| Padmanabh Dabke| author meta-tag in index.html|
|  EMAIL_LOGO_URL| /images/app_logo.png| Logo URL in the email template. You can either specify an absolute URL or a URI relative to CDN_URL.|
|  PERISHABLE_CACHE_MAX_SIZE| 500| Maximum cache size for the cache that stores items that expire after short time|
|  PERISHABLE_CACHE_MAX_AGE| 300000| Age of perishable cache items in seconds|
|  REMEMBER_ME_SESSION_TIMEOUT| 2592000| Longer session timeout, defined in seconds, in "Remember Me" login mode|
|  SESSION_TIMEOUT| 3600| Session timeout in seconds |
|  LAST_ACCESS_REFRESH_INTERVAL| 60| Period in seconds for updating last access time and evaluating session timeouts| 
|  SESSION_COOKIE_NAME| sksession| Session cookie name|
