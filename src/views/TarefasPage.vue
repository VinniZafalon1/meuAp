<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>

        <ion-buttons slot="start">
          <ion-back-button default-href="/"></ion-back-button>
        </ion-buttons>

        <ion-title>Tarefas</ion-title>

      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">

      <!-- ADICIONAR -->
      <ion-card>
        <ion-card-header>
          <ion-card-title>Nova tarefa</ion-card-title>
        </ion-card-header>

        <ion-card-content>
          <ion-item>

            <ion-input
              v-model="novaTarefa"
              placeholder="Digite uma tarefa..."
            />

            <ion-button @click="adicionarNova">
              <ion-icon :icon="add"></ion-icon>
            </ion-button>

          </ion-item>
        </ion-card-content>
      </ion-card>

      <!-- BUSCA -->
      <ion-item>
        <ion-input
          v-model="busca"
          placeholder="Buscar tarefas..."
        />
      </ion-item>

      <!-- FILTRO -->
      <ion-segment v-model="filtroAtivo">

        <ion-segment-button value="todas">
          <ion-label>Todas</ion-label>
        </ion-segment-button>

        <ion-segment-button value="pendentes">
          <ion-label>Pendentes</ion-label>
        </ion-segment-button>

        <ion-segment-button value="feitas">
          <ion-label>Feitas</ion-label>
        </ion-segment-button>

      </ion-segment>

      <!-- LISTA -->
      <CardTarefa
        v-for="tarefa in filtradas"
          :key="tarefa.id"
          :tarefa="tarefa"
        @click="abrirDetalhe(tarefa.id)"
        @remover="remover"
        @concluir="concluir"
/>
      

      <!-- STATUS -->
      <ion-card v-if="filtradas.length === 0">
        <ion-card-content class="ion-text-center">
          Nenhuma tarefa encontrada.
        </ion-card-content>
      </ion-card>

      <!-- CONTADOR -->
      <ion-text class="contador">
        Pendentes: {{ totalPendentes }}
      </ion-text>

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

import { add } from "ionicons/icons";

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonInput,
  IonItem,
  IonButton,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonSegment,
  IonSegmentButton,
  IonLabel,
  IonText,
  IonIcon,
  IonButtons,
  IonBackButton,
} from "@ionic/vue";

import CardTarefa from "../components/CardTarefa.vue";
import { useTarefas } from "../composables/useTarefas";

const router = useRouter();

const {
  busca,
  filtroAtivo,
  filtradas,
  totalPendentes,
  adicionar,
  remover,
  concluir,
} = useTarefas();

const novaTarefa = ref("");

function adicionarNova() {
  if (!novaTarefa.value.trim()) return;

  adicionar(novaTarefa.value);
  novaTarefa.value = "";
}

function abrirDetalhe(id: number) {
  router.push(`/tabs/tarefas/${id}`);
}
</script>

<style scoped>
ion-card {
  margin-bottom: 16px;
}

ion-item {
  --inner-padding-end: 6px;
}

ion-segment {
  margin: 16px 0;
}

.contador {
  display: block;
  margin-top: 16px;
  font-size: 14px;
  opacity: 0.7;
}

ion-button {
  height: 36px;
}

.ion-text-center {
  text-align: center;
}
</style>