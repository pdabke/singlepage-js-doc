# Creating Custom Look & Feel
## CSS Framework
`singlepage-js` uses Bootstrap framework for styling portal presentation. There are a few important changes are worth noting. We
have removed `lg` and `xl` media breakpoints and only use `sm` and `md` breakpoints and corresponding classes in our
presentation. Also, we do not use bootstrap's Javascript code or jquery. We have replaced some of the essential functionality
by writing our own code or using vue plug-ins or libraries. 

The `src/css` directory in your application folder contains 
four CSS files:
- bootstrap-reboot.css - Style resets for browser consistency and styling of basic html elements
- bootstrap-grid.css - Grid and spacing classes
- bootstrap.css - Themable classes defining major colors and component styles
- sp.css - `singlepage-js` system classes needed for system components and certain layout preferences

We recommend that you do not change reboot and grid classes unless you know what you are doing. `bootstrap.css` contains all themable
classes and should be the main focus for look & feel customization. You can modify sp.css classes to change overall page display (sticky 
footer), system components styling (e.g. sidebar menu on smaller displays).

## Images
`singlepage-js` uses three images located in `assets` and `assets/images` directories that can be replaced by your own: favicon.ico, 
avatar.png, and app_logo.png. `app_logo.png` is the main logo image that is used on the splash screen, Web site logo displayed at top
left once the application is loaded, login and logout screens, and the service_tester utility. Simplest change would be to replace 
this with your own. In order to display a different image for different screens, you will have to change the corresponding Vue components
(App.vue, Login.vue, Logout.vue) or HTML files (index.html, service_tester.html).

## Portal Window Styling
The appearance of components on the portal can be controlled by setting component wrapper, header, and body CSS classes. `singlepage-js` 
comes with built-in templates. The built-in template definitions are shown below.
```json
{

  "card-default": { "componentClass": "card sp-card flex-grow-1", "headerClass": "card-header bg-light h5", "bodyClass": "card-body" },
  "card-flush": { "componentClass": "card sp-card flex-grow-1", "headerClass": "card-header bg-light h5", "bodyClass": "" },
  "note-default": { "componentClass": "card sp-card flex-grow-1", "headerClass": "card-header border-0 bg-white h5", "bodyClass": "card-body" },
  "note-flush": { "componentClass": "card sp-card flex-grow-1", "headerClass": "card-header border-0 bg-white h5", "bodyClass": "" },
  "blank": { "componentClass": "flex-grow-1 position-relative", "headerClass": "", "bodyClass": "" },
  "jumbotron": { "componentClass": "jumbotron position-relative flex-grow-1", "headerClass": "display-4", "bodyClass": "" },
  "borderless": { "componentClass": "card border-0 flex-grow-1", "headerClass": "bg-white h4 pt-2 pb-2  border-bottom", "bodyClass": "" },
  "flush": { "componentClass": "card sp-card flex-grow-1", "headerClass": "card-header", "bodyClass": "" },
  "card-warning": { "componentClass": "card alert-warning flex-grow-1", "headerClass": "card-header h5", "bodyClass": "card-body bg-white" },
  "note-warning": { "componentClass": "card-body alert-warning position-relative flex-grow-1", "headerClass": "h5", "bodyClass": "" },
  "card-info": { "componentClass": "card alert-info flex-grow-1", "headerClass": "card-header h5", "bodyClass": "card-body bg-white" },
  "note-info": { "componentClass": "card-body alert-info position-relative flex-grow-1", "headerClass": "h5", "bodyClass": "" },
  "card-dark": { "componentClass": "card alert-dark flex-grow-1", "headerClass": "card-header h5", "bodyClass": "card-body" },
  "note-dark": { "componentClass": "card-body alert-dark position-relative flex-grow-1", "headerClass": "h5", "bodyClass": "" },
  "card-light": { "componentClass": "card alert-light flex-grow-1", "headerClass": "card-header h5", "bodyClass": "card-body" },
  "note-light": { "componentClass": "card-body alert-light position-relative flex-grow-1", "headerClass": "h5", "bodyClass": "" },
  "card-success": { "componentClass": "card alert-success flex-grow-1", "headerClass": "card-header h5", "bodyClass": "card-body bg-white" },
  "note-success": { "componentClass": "card-body alert-success position-relative flex-grow-1", "headerClass": "h5", "bodyClass": "" },
  "card-danger": { "componentClass": "card alert-danger flex-grow-1", "headerClass": "card-header h5", "bodyClass": "card-body bg-white" },
  "note-danger": { "componentClass": "card-body alert-danger position-relative flex-grow-1", "headerClass": "h5", "bodyClass": "" }
}
```
You can add to these or overwrite existing template definitions by creating `component_templates.json` file in `<app-root>/src/templates`
directory. A sample JSON file is shown below. The file shown will overwrite styling of `card-default` template and add a new template 
named `note-padded-centered`.

```json
    {
      "card-default": {
        "componentClass": "card sp-card flex-grow-1",
        "headerClass": "card-header bg-secondary h5",
        "bodyClass": "card-body"
      },
      "note-padded-centered": {
        "componentClass": "card sp-card flex-grow-1",
        "headerClass": "card-header border-0 bg-white h5",
        "bodyClass": "p-5 d-flex align-items-center justify-content-center"
      }
    }
```
## Page Layouts
When you create a new page in `singlepage-js`, you can select the page layout: 2-columns, 3-columns, etc. `singlepage-js` defines a set of
default page layouts. The layout definition files are located in `<singlepage-js-install-dir>/dev/resources/page_templates` directory.
Contents of `page_narrow_wide.xml` file are listed below.
```xml
    <div class="container mt-3">
        <div class="row">
            <div class="col-md-4">
            </div>
            <div class="col-md-8">
            </div>
        </div>
    </div>
```

As you can see, a page layout definition file is an XML file that provides the skeleton for the layout. You can use any bootstrap spacing or grid-related
classes to get the desired result. You can create your own layouts by creating similar files that start with `page_` in `<app-root-dir>/src/templates`
directory and they will appear in the page layout dropdown on page create/edit screens. You can also overwrite existing page layout definitions by placing
a file with the same name as the original file name.
