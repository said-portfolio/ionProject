<template>
  <ion-page>
    <body>
      <ion-header :translucent="true">
        <ion-toolbar>
          <ion-row class="toolBar">
            <ion-col size="4" size-md="8" size-lg="10">
              <ion-title>Blank</ion-title>
            </ion-col>
            <ion-col size="8" size-md="4" size-lg="2"
            ><ion-grid>
              <ion-row class="themeBar">
                <ion-col class="light-mode-icon">
                  <ion-icon :src="require('@/assets/icons/light.svg')" />
                </ion-col>
                <ion-col class="toggle-icon">
                  <ion-toggle @ionChange="toggle()" :checked="isDark" />
                </ion-col>
                <ion-col class="dark-mode-icon">
                  <ion-icon :src="require('@/assets/icons/dark.svg')" />
                </ion-col>
              </ion-row>
            </ion-grid>
          </ion-col>
          </ion-row>
        </ion-toolbar>
      </ion-header>

      <ion-content>
        {{ isDark }}
      </ion-content>
    </body>
  </ion-page>
</template>

<script setup>
import { useDark, useToggle } from "@vueuse/core";
import {
  IonPage,
  IonContent,
  IonHeader,
  IonTitle,
  IonToolbar,
  IonToggle,
  IonIcon,
  IonGrid,
  IonRow,
  IonCol,
} from "@ionic/vue";
import { watchEffect } from "vue";

const isDark = useDark();
const toggle = useToggle(isDark);

watchEffect(() => {
  document.body.setAttribute(
    "color-mode",
    isDark.value === true ? "dark" : "auto"
  );
});
</script>

<style lang="scss" scoped>
.toolBar {
  display: flex;
  justify-content: baseline;
  align-items: center;
}
.themeBar{
  display: flex;
  align-items: center;
  text-align: center;
  .light-mode-icon {
    text-align: right;
  }
  .dark-mode-icon {
    text-align: left;
  }
  .toggle-icon {
    text-align: center;
  }
}
</style>
