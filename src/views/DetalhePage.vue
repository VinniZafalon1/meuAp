<template>
  <IonPage>

    <IonHeader>
      <IonToolbar>

        <IonButtons slot="start">
          <IonBackButton default-href="/tabs/tarefas" />
        </IonButtons>

        <IonTitle>Detalhes da Tarefa</IonTitle>

      </IonToolbar>
    </IonHeader>

    <IonContent class="ion-padding">

      <div v-if="tarefa">

        <h2>{{ tarefa.titulo }}</h2>

        <p>
          Status:
          {{ tarefa.concluida ? 'Concluída' : 'Pendente' }}
        </p>

        <IonButton
          expand="block"
          color="success"
          @click="concluirTarefa"
        >
          Concluir tarefa
        </IonButton>

<IonButton
  expand="block"
  color="danger"
  @click="confirmarExclusao"
>
  Excluir tarefa
</IonButton>

      </div>

      <div v-else>
        <p>Tarefa não encontrada.</p>
      </div>

    </IonContent>

  </IonPage>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useRoute } from 'vue-router'

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonButton,
  useIonRouter,
  alertController
} from '@ionic/vue'

const route = useRoute()
const ionRouter = useIonRouter()

// pega as tarefas salvas
const tarefas = JSON.parse(
  localStorage.getItem('tarefas') || '[]'
)

// pega o id da URL
const id = Number(route.params.id)

// encontra a tarefa
const tarefa = computed(() =>
  tarefas.find((t: any) => t.id === id)
)

// concluir tarefa
function concluirTarefa() {

  const index = tarefas.findIndex(
    (t: any) => t.id === id
  )

  if (index !== -1) {

    tarefas[index].concluida = true

    localStorage.setItem(
      'tarefas',
      JSON.stringify(tarefas)
    )

    alert('Tarefa concluída!')
  }
}

// excluir tarefa com confirmação
async function confirmarExclusao() {

  const alert = await alertController.create({
    header: 'Excluir tarefa?',
    message: 'Essa ação não pode ser desfeita.',

    buttons: [
      {
        text: 'Cancelar',
        role: 'cancel'
      },

      {
        text: 'Excluir',
        role: 'destructive',

        handler: () => {

          const novasTarefas = tarefas.filter(
            (t: any) => t.id !== id
          )

          localStorage.setItem(
            'tarefas',
            JSON.stringify(novasTarefas)
          )

          ionRouter.push('/tabs/tarefas')
        }
      }
    ]
  })

  await alert.present()
}
</script>