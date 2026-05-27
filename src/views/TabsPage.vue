<template>
  <IonPage>

    <IonTabs>

      <!-- páginas -->
      <IonRouterOutlet />

      <!-- barra inferior -->
      <IonTabBar slot="bottom">

        <IonTabButton
          tab="home"
          href="/tabs/home"
        >
          <IonIcon :icon="homeOutline" />
          <IonLabel>Home</IonLabel>
        </IonTabButton>

        <IonTabButton
          tab="tarefas"
          href="/tabs/tarefas"
        >
          <IonIcon :icon="listOutline" />
          <IonLabel>Tarefas</IonLabel>
        </IonTabButton>

        <IonTabButton
        tab="perfil"
        href="/tabs/perfil"
>
        <IonIcon :icon="personOutline" />
        <IonLabel>Perfil</IonLabel>
        </IonTabButton>

      </IonTabBar>

    </IonTabs>

  </IonPage>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonTabs,
  IonRouterOutlet,
  IonTabBar,
  IonTabButton,
  IonLabel,
  IonIcon
} from '@ionic/vue'

import {
  homeOutline,
  listOutline,
  personOutline
} from 'ionicons/icons'
</script>