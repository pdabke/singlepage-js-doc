# Quick Start
## Installation
Install `singlepage-js` globally.
```console
$ npm install -g singlepage-js
```
## Application Setup
Global installation of singlepage-js provides the `singlepage` command that can be used to generate application boilerplate and serve your application. You can create application boilerplate code via `create` command and serve your application via `serve` command.

```console
$ singlepage create myapp
$ cd myapp
$ singlepage serve

```
## View Application
Open a Web browser and access your application on http://localhost:8080. 

## Edit Application
Click on the Login button on the top right corner. Use admin/admin as your username/password. The Login button will be replaced by a button that shows current user information. Click on the button and select `Turn on Edit Mode`. This will show editing commands in the same dropdown. It also shows a gear icon and a drag icon on each portal window (component). The following is a quick summary of supported edit operations:

- Add Component: Each column in the grid shows a select box with `Add` button next to it. Select the component you want to add from the select dropdown and click `Add` to add that component to the column
- Edit Component Properties: Click on the gear icon on a portal window and select "Edit Settings" to set component properties
- Delete Component: Select "Delete Component" from the portal window menu 
- Rearrange Components: You can drag and drop components by clicking on the drag icon on the portal window
- Add Page: Select "New Page" from the top right dropdown and enter requested page metadata
- Delete Page: Select "Delete Current Page" from the top level dropdown
- Change Page Order: Drag and drop the top menubar page links to the desired position
- Add Folder: Open Page Manager by selecting `Page Manager` option from the top portal menu and click on "New Folder" button


## Build Application
Use `build` command to create your distribution. The distribution is created in the `dist` folder under your application directory. You can use `spstart.js`  script in the `bin` directory to run the server.

```console
$ cd myapp
$ singlepage build
$ node ./dist/bin/spstart.js
```
## Deploy Application
You can simply copy the dist directory to your production environment to deploy it. Additional steps such as installing node and running `npm install` may be needed depending on your hosting provider and your method of deployment. See `Application Deployment` section for details how to deploy on cloud.
