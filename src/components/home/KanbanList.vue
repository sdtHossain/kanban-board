<script setup lang="ts">
import { onMounted, ref } from 'vue'
interface taskType {
  id: number
  title: String
}
const props = defineProps({
  title: {
    type: String,
    default: 'Title'
  },
  items: {
    type: Array<taskType>,
    default: [{}]
  },
  id: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['filterTask', 'dragEvent', 'addItemToList'])

const tasks = ref<Array<HTMLElement>>([])

// onMounted(() => {
//   // console.log(tasks.value)
//   tasks.value.forEach((item) => {
//     item.addEventListener('dragstart', (e) => {
//       console.log(e)
//     })
//   })
// })

const droppedItem = ref<object>({})
const draggedItemType = ref<String>('')
const droppedToItemsType = ref<String>('')

const dragstart = (item: object, id: String, index: number) => {
  // console.log(item, id)
  emit('dragEvent', item, id)
  tasks.value[index].classList.add('moving')
}

const dropEvent = (droppToId: String) => {
  // console.log(item, droppToId)
  emit('filterTask', droppToId)
}

const newTask = ref()
const newTaskId = ref()
</script>
<template>
  <div @dragover.prevent @drop="dropEvent(id)" class="kanban-column">
    <div class="kanban-header">{{ title }}</div>
    <div
      class="kanban-item"
      v-for="(item, index) in items"
      :key="index"
      ref="tasks"
      draggable="true"
      @dragstart="dragstart(item, id, index)"
    >
      Task {{ index + 1 }}: {{ item.title }}
    </div>
    <div class="kanban-footer">
      <div class="card p-3">
        <form action="" @submit.prevent>
          <p>
            <input type="text" v-model="newTaskId" placeholder="task id" class="form-control" />
          </p>
          <p>
            <input
              type="text"
              v-model="newTask"
              placeholder="Enter new task"
              class="form-control"
            />
          </p>
          <button
            @click="$emit('addItemToList', { newTaskId, newTask, id })"
            class="btn btn-primary"
          >
            Add
          </button>
        </form>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
