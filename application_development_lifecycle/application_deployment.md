# Application Deployment
## Build Application
Use `singlepage build` command to create your distribution. The distribution is created in the `dist` folder under your application directory. You can use `spstart.js`  script in the `bin` directory to run the server and see your application in action locally.

```console
$ cd myapp
$ singlepage build
$ node ./dist/bin/spstart.js
```
## Deploy Application
In general, you can simply copy the dist directory to your production environment to deploy it. Additional steps such as installing node and running `npm install` may be needed depending on your hosting provider and your method of deployment. Singlepage relies on some environment variables that control aspects of its runtime behavior. We recommend using your hosting providers mechanism for setting these environment variables but you can also define them in the .env file in the root directory of your distribution. The environment variables recognized by Singlepage are listed below.
### Environment variables
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

### Deploy Application to Heroku
Heroku uses git to push a Web application for deployment, so you will need both git and Heroku CLI to complete the deployment step below.

Log in to heroku
```console
$ heroku login -i
heroku: Enter your login credentials
Email :you@example.com
Password: ************
Logged in as you@example.com

$ heroku whoami
you@example.com
```
Build your app
```console
$ cd myapp
$ singlepage build
$ cd dist

```
Create .gitignore file and Procfile at the top level in dist directory
```console
$ more Procfile
web: node ./bin/spstart.js

$ more .gitignore
.DS_Store
node_modules
/dist
.env*

```
Create local Git and commit code in dist
```console
$ git init
Initialized empty Git repository in /projects/myapp/dist/.git/

$ git add --all

$git commit -m "Initial commit"
[master (root-commit) 6f183fd] Initial commit
 33 files changed, 555 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 Procfile
 create mode 100644 bin/spstart.js
     :
     :
```
Create Heroku app and deploy your code to Heroku by pushing it to the remote Git repository
```console
$ heroku create -a singlepage-app-test
Creating singlepage-app-test... done
https://singlepage-app-test.herokuapp.com/ | https://git.heroku.com/singlepage-app-test.git

$ git remote -v
heroku  https://git.heroku.com/singlepage-app-test.git (fetch)
heroku  https://git.heroku.com/singlepage-app-test.git (push)

$ git push heroku master
Enumerating objects: 45, done.
Counting objects: 100% (45/45), done.
Delta compression using up to 12 threads
Compressing objects: 100% (39/39), done.
Writing objects: 100% (45/45), 116.58 KiB | 6.48 MiB/s, done.
Total 45 (delta 5), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Node.js app detected
remote:
remote: -----> Creating runtime environment
remote:
remote:        NPM_CONFIG_LOGLEVEL=error
remote:        NODE_ENV=production
remote:        NODE_MODULES_CACHE=true
remote:        NODE_VERBOSE=false
remote:
remote: -----> Installing binaries
remote:        engines.node (package.json):  10.x
remote:        engines.npm (package.json):   unspecified (use default)
remote:
remote:        Resolving node version 10.x...
remote:        Downloading and installing node 10.16.3...
remote:        Using default npm version: 6.9.0
remote:
remote: -----> Installing dependencies
remote:        Installing node modules (package.json)
remote:        added 9 packages from 9 contributors and audited 9 packages in 0.87s
remote:        found 0 vulnerabilities
remote:
remote:
remote: -----> Build
remote:
remote: -----> Pruning devDependencies
remote:        removed 1 package and audited 8 packages in 0.591s
remote:        found 0 vulnerabilities
remote:
remote:
remote: -----> Caching build
remote:        - node_modules
remote:
remote: -----> Build succeeded!
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote:
remote: -----> Compressing...
remote:        Done: 19.6M
remote: -----> Launching...
remote:        Released v3
remote:        https://singlepage-app-test.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/singlepage-app-test.git
 * [new branch]      master -> master
```