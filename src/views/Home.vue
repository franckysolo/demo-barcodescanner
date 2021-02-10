<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title v-html="title" />
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large" v-html="title" />
        </ion-toolbar>
      </ion-header>
      <div id="container" class="ion-padding ion-text-center">
        <ion-button @click="scanBarcode" v-html="label" />
        <pre>
          {{ code }}
        </pre>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonButton
} from '@ionic/vue'

import { defineComponent, ref } from 'vue'

import { Plugins } from '@capacitor/core'
const { MlkitBarcodescanner } = Plugins

export default defineComponent({
  name: "Home",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton
  },
  setup() {
    const code = ref(null)
    const scanBarcode = async () => {
      let result = await MlkitBarcodescanner.scanBarcode()
      console.log(result)
      code.value = result
    }

    return {
      code,
      scanBarcode,
      label: "Scanner un code barre",
      title: "Barcodescanner"
    }
  },
})
</script>

<style scoped>
</style>
