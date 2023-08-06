<template>
  <ion-app>
    <ion-router-outlet v-if="connected"/>
    <login-view v-else @loginEmited="connected = true"></login-view>
  </ion-app>
</template>

<script>
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import LoginView from './components/LoginView.vue';

export default {
  components: {
    IonApp,
    IonRouterOutlet,
    LoginView
  },
  data() {
    return {
      connected: true
    };
  }
}
</script>
