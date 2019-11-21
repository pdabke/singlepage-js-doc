# Environment variables
Singlepage relies on some environment variables that control aspects of its 
runtime behavior. We recommend using your hosting provider's mechanism for
setting these environment variables but you can also define them in .env* 
files. During development time, `singlepage serve` will pick up the environment
properties from .env.development file; if that does not exist it will load it
from .env file. When `singlepage build` creates the app
distribution, it will copy your .env.production file (or .env file if it does 
not exist) to .env file in the distribution root directory.

The environment variables recognized by Singlepage are listed below.

|Variable|Description|
|--------|-----------|
|PORT| HTTP Port  |
|HTTPS_PORT| HTTPS Port. Only needed if the server is not running behind a proxy or you want the communication between the server and proxy to be encrypted as well.
|HTTPS_CERT|Path to the HTTPS certificate file or Base64 encoded certificate|
|HTTPS_KEY|Path to the certificate key file or Base64 encoded key|
NODE_ENV| Must be set to `production` or unset|
|SP_USER_NAME|Admin user login name. Applicable only in the single user mode|
|SP_PASSWORD|Admin user password. Applicable only in the single user mode|
|SP_SESSION_KEY|Session key used to encrypt session cookie. Must be 8 alphanumeric characters|
|SMTP_HOST| Host address of SMTP server|
|SMTP_PORT| SMTP server port|
|SMTP_USER| SMTP connection user name|
|SMTP_PASSWORD| SMTP connection password|