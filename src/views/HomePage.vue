<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar color="danger">
        <ion-title>Stock Plus</ion-title>
        <ion-button color="success" @click="addProduct" slot="secondary">
          <ion-icon :icon="add" slot="icon-only"></ion-icon>
        </ion-button>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <input color="medium" placeholder="Search Product........" v-model="searchValue"/>
      <ion-icon :icon="search" size="medium"></ion-icon>
      <ion-list>
        <ion-item> 
          <ion-avatar slot="start" @click="viewProfile">
            <img src="../assets/alicia_keys.jpg" id="open-modal-img"/>
          </ion-avatar>
          <ion-label @click="showProduct = true">
            <h2>Product name here...</h2>
            <p>Informations here...</p>
          </ion-label>
          <ion-button color="success" @click="editProduct">
            <ion-icon slot="icon-only" :icon="create"></ion-icon>
          </ion-button>
          <ion-button color="danger" @click="deleteProduct()">
            <ion-icon slot="icon-only" :icon="trash"></ion-icon>
          </ion-button>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar
} from '@ionic/vue';

import { person, create, add, trash, checkmark, calendar, search } from 'ionicons/icons';
import AddProductModal from '../components/AddProductModal.vue';

export default {
  data() {
    return {
      person,
      create,
      add,
      trash,
      checkmark,
      calendar,
      search,
      searchValue: '',
      products: []
    }
  },  
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
  },
  methods: {
    async addProduct() {
      const modal = await modalController.create({
        component: AddProductModal,
        componentProps: {
          titleProps: "Add Product"
        }
      });
      modal.present();

      const { data, role } = await modal.onWillDismiss();

      if (role === 'confirm') {
        this.products = data
      }
    },
  }
}
</script>

<style scoped>
#container {
  text-align: center;  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
