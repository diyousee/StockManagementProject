<template>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-button color="medium" @click="cancel">Cancel</ion-button>
        </ion-buttons>
        <ion-title>{{ titleProps }}</ion-title>
        <ion-buttons slot="end">
          <ion-button @click="confirm" :strong="true">Confirm</ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
        <ion-item fill="outline">
            <ion-label position="floating">Product Name</ion-label>
            <ion-input type="text" v-model="product_name"></ion-input>
            <span v-if="product_name.trim() === ''" class="error_msg">{{ msg }}</span>
        </ion-item>
        <br>
        <ion-item fill="outline">
            <ion-label position="floating">Purchase Price</ion-label>
            <ion-input type="text" v-model="purchase_price"></ion-input>
            <span v-if="purchase_price.trim() === ''" class="error_msg">{{ msg }}</span>
        </ion-item>
        <br>
        <ion-item fill="outline">
            <ion-label position="floating">Sale Price</ion-label>
            <ion-input type="text" v-model="sale_price"></ion-input>
            <span v-if="sale_price.trim() === ''" class="error_msg">{{ msg }}</span>
        </ion-item>
        <br>
    </ion-content>
</template>

<script>
  import {
    IonContent,
    IonHeader,
    IonTitle,
    IonToolbar,
    IonButtons,
    IonButton,
    IonItem,
    IonInput,
    modalController
  } from '@ionic/vue';

  export default ({
    name: 'AddProductModal',
    props: ['titleProps'],
    components: { 
        IonContent,
        IonHeader,
        IonTitle,
        IonToolbar,
        IonButtons,
        IonButton,
        IonItem,
        IonInput
    },
    data(){
        return {
          products: [],
          product_name: "",
          purchase_price: "",
          sale_price: "",
          msg: "",
        };
    },
    mounted(){
      var listeE = localStorage.getItem("productsList")

      if(listeE){
        this.products=JSON.parse(listeE)
      }
    },
    methods: {
      cancel() {
        return modalController.dismiss(null, 'cancel');
      },
      confirm() {
        let product = {
            product_name: this.product_name,
            purchase_price: this.purchase_price,
            sale_price: this.sale_price,
        }
        
        if(this.product_name.trim() !== "" && this.purchase_price.trim() !== "" && this.sale_price.trim() !== ""){
            
          this.products.push(product);
          localStorage.setItem("productsList", JSON.stringify(this.products))           

          return modalController.dismiss(this.products, 'confirm');
        }else{
          this.msg= 'Complete this field'
        }
      },
    },
  });
</script>

<style scoped>
.error_msg{
    color: rgb(255, 0, 0);
    text-align: center;
    padding: 5px;
    font-size: 10px;
}
</style>