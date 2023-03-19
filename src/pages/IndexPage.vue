<template>
  <q-page class="flex items-center column">
    <h4>Lista de Tarefas</h4>
    <div class="flex">
      <q-input
      v-model="taskInput"
            type="text" label="Nome da tarefa"
            outlined class="q-mr-sm"
            @keyup.enter="add"
            > </q-input>
      <q-btn label="Adicionar" @click="add" color="blue-12"></q-btn>
    </div>
    <div class="q-mt-md" style="width:450px" v-if="itemsList.length>0">
      <q-list bordered padding>

      <q-item tag="label" v-ripple v-for="item in orderedItemsList" :key="item.id">
        <q-item-section side >
          <q-checkbox v-model="item.done" />
        </q-item-section>

        <q-item-section>
          <q-item-label>{{item.name}}</q-item-label>
          <!-- <q-item-label caption>
            {{item.description}}
          </q-item-label> -->
        </q-item-section>

        <q-item-section side avatar>
          <!-- <q-icon name="delete" color="red" /> -->
          <q-btn icon="delete" flat  @click="removeTask(item)" color="red-12"></q-btn>
        </q-item-section>
      </q-item>

      </q-list>
    </div>
    <div v-else>
        <h6 >Sem tarefas</h6>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data () {
    return {
      taskInput: '',
      check1: true,
      check2: false,
      check3: false,
      itemsList: []
    }
  },
  methods: {
    add () {
      this.itemsList.push({ id: (this.itemsList.length + 1), name: this.taskInput, description: '', done: false })
      this.taskInput = ''
    },
    removeTask (item) {
      this.itemsList = this.itemsList.filter((i) => {
        return i.id !== item.id
      })
    }
  },
  computed: {
    orderedItemsList () {
      const items = this.itemsList
      return items.sort(function (a, b) {
        if (a.id < b.id) {
          return 1
        }
        if (a.id > b.id) {
          return -1
        }
        return 0
      })
    }
  }
})
</script>
