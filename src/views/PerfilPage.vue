<template>
  <IonPage>

    <IonHeader>
      <IonToolbar>
        <IonTitle>Perfil</IonTitle>
      </IonToolbar>
    </IonHeader>

    <IonContent class="ion-padding">

      <IonInput
        v-model="nome"
        placeholder="Digite seu nome"
      />

      <IonButton
        expand="block"
        @click="salvarNome"
      >
        Salvar
      </IonButton>

      <p v-if="mensagem">
        {{ mensagem }}
      </p>

    </IonContent>

  </IonPage>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonInput,
  IonButton
} from '@ionic/vue'

const nome = ref('')
const mensagem = ref('')

// carrega nome salvo
onMounted(() => {

  const nomeSalvo = localStorage.getItem('nome')

  if (nomeSalvo) {
    nome.value = nomeSalvo
  }
})

// salva nome
function salvarNome() {

  if (!nome.value.trim()) {

    mensagem.value = 'Digite um nome.'

    return
  }

  localStorage.setItem('nome', nome.value)

  mensagem.value = 'Nome salvo com sucesso!'
}
</script>