<template>
  <f7-app v-bind="f7params">

  <!-- Left panel with cover effect when hidden -->
  <f7-panel left cover :visible-breakpoint="960" dark>
    <f7-view>
      <f7-page>
        <f7-navbar title="Menü"></f7-navbar>
        <!--f7-block-title>Látogatóknak</f7-block-title-->
        <f7-list>
          <f7-list-item link="/textview/about/" view=".view-main" panel-close title="A Mohács Infó App-ról"></f7-list-item>
          <f7-list-item link="/favorites/" view=".view-main" panel-close title="Kedvenc tel. számaim"></f7-list-item>
        </f7-list>

        <f7-block-title>Tagoknak</f7-block-title>
        <f7-list>
          <f7-list-item link="/signin/" view=".view-main" panel-close title="Bejelentkezés"></f7-list-item>
          <f7-list-item link="/signup/" view=".view-main" panel-close title="Regisztráció"></f7-list-item>
          <!--f7-list-item link="/signout/" view=".view-main" panel-close title="Regisztráció"></f7-list-item-->
          <!--f7-list-item link="#" view=".view-main" back panel-close title="Elfelejtett jelszó"></f7-list-item-->
        </f7-list>

      </f7-page>
    </f7-view>
  </f7-panel>

  <!-- Right panel with reveal effect-->
  <!--f7-panel right reveal dark>
    <f7-view>
      <f7-page>
        <f7-navbar title="Right Panel"></f7-navbar>
        <f7-block>Right panel content goes here</f7-block>
      </f7-page>
    </f7-view>
  </f7-panel-->

  <!-- Your main view, should have "view-main" class -->
  <f7-view main class="safe-areas" url="/"></f7-view>


    <!-- Popup -->
<!--
    <f7-popup id="my-popup">
      <f7-view>
        <f7-page>
          <f7-navbar title="Popup">
            <f7-nav-right>
              <f7-link popup-close>Close</f7-link>
            </f7-nav-right>
          </f7-navbar>
          <f7-block>
            <p>Popup content goes here.</p>
          </f7-block>
        </f7-page>
      </f7-view>
    </f7-popup>

    <f7-login-screen id="my-login-screen">
      <f7-view>
        <f7-page login-screen>
          <f7-login-screen-title>Login</f7-login-screen-title>
          <f7-list form>
            <f7-list-input
              type="text"
              name="username"
              placeholder="Your username"
              v-model:value="username"
            ></f7-list-input>
            <f7-list-input
              type="password"
              name="password"
              placeholder="Your password"
              v-model:value="password"
            ></f7-list-input>
          </f7-list>
          <f7-list>
            <f7-list-button title="Sign In" @click="alertLoginData"></f7-list-button>
            <f7-block-footer>
              Some text about login information.<br>Click "Sign In" to close Login Screen
            </f7-block-footer>
          </f7-list>
        </f7-page>
      </f7-view>
    </f7-login-screen>
-->
	
  </f7-app>
</template>
<script>
  import { ref, onMounted } from 'vue';
  import { f7, f7ready } from 'framework7-vue';
  import { getDevice }  from 'framework7/lite-bundle';
  import cordovaApp from '../js/cordova-app.js';

  import routes from '../js/routes.js';
  import store from '../js/store';

  export default {
    setup() {
      const device = getDevice();
      // Framework7 Parameters
      const f7params = {
        name: 'My Fuelings', 	// App name
        theme: 'auto', 			// Automatic theme detection


        id: 'io.framework7.fuelings.my', // App bundle ID
        // App store
        store: store,
        // App routes
        routes: routes,


        // Input settings
        input: {
          scrollIntoViewOnFocus: device.cordova && !device.electron,
          scrollIntoViewCentered: device.cordova && !device.electron,
        },
        // Cordova Statusbar settings
        statusbar: {
          iosOverlaysWebView: true,
          androidOverlaysWebView: false,
        },
      };
      // Login screen data
      const username = ref('');
      const password = ref('');

      const alertLoginData = () => {
        f7.dialog.alert('Username: ' + username.value + '<br>Password: ' + password.value, () => {
          f7.loginScreen.close();
        });
      }
      onMounted(() => {
        f7ready(() => {
          // Init cordova APIs (see cordova-app.js)
          if (device.cordova) {
            cordovaApp.init(f7);
          }

          // Call F7 APIs here
        });
      });

      return {
        f7params,
        username,
        password,
        alertLoginData
      }
    }
  }
</script>