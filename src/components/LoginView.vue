<template>
    <ion-page>
        <ion-content class="ion-padding">
            <ion-item fill="outline">
                <ion-label position="floating">Username</ion-label>
                <ion-input type="text"></ion-input>
            </ion-item>
            <br>
            <ion-item fill="outline">
                <ion-label position="floating">Password</ion-label>
                <ion-input type="password"></ion-input>
            </ion-item>
            <br>
            <ion-button expand="block" @click="$emit('loginEmited')">Connexion</ion-button>
        </ion-content>
    </ion-page>
</template>

<script>
import { IonPage, IonContent, IonItem, IonLabel, IonInput, IonButton } from "@ionic/vue"

export default {
    components: {
        IonPage,
        IonContent,
        IonItem,
        IonLabel,
        IonInput,
        IonButton
    },
    name: 'LoginView',
    data() {
        return {

        };
    },
};
</script>

<style scoped>

</style>