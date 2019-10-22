# Overwriting System Components
`singlepage-js` allows you replace four default system components by your own: App.vue, Login.vue, Logout.vue, PageNotFound.vue. The best way to 
customize system components to create your application boilerplate using `singlepage create myapp -f`. The `-f` flag writes a copy of default
Vue components to the `src` directory. You can then modify these components according to your needs. Note that your `main.js` file looks a little
different when you want to use your own components. More specifically, you have to supply your components to the `init` method on SPApp object:
```js
"use strict";
import Vue from 'vue';
import SPApp from '../lib/splib.esm.js';
import App from './App.vue';
import Login from './Login.vue';
import Logout from './Logout.vue';
import PageNotFound from './PageNotFound.vue';
import './www/css/bootstrap-reboot.css'
import './www/css/bootstrap-grid.css'
import './www/css/bootstrap.css'
import './www/css/sp.css';

Vue.config.productionTip = false;

SPApp.init(SP_CONFIG, SP_MESSAGES, SP_COMPONENT_TEMPLATES, App, Login, Logout, PageNotFound);
```