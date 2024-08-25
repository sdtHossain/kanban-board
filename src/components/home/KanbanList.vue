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

const emit = defineEmits(['onDragStartEvent', 'onDropEvent', 'onDragEndEvent', 'inDropToColumn'])

const newTask = ref()
const newTaskId = ref()
</script>
<template>
  <div
    @dragover.prevent
    @drop="$props.items?.length! < 1 && $emit('inDropToColumn', id)"
    class="kanban-column"
  >
    <div class="kanban-header">{{ title }}</div>
    <div
      class="kanban-item"
      v-for="(item, index) in items"
      :key="index"
      draggable="true"
      @dragstart="$emit('onDragStartEvent', { item, index, id })"
      @drop="$emit('onDropEvent', $event, { index, id })"
      @dragend="$emit('onDragEndEvent')"
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
          <button class="btn btn-primary">Add</button>
        </form>
      </div>
    </div>
  </div>
</template>
<style scoped></style>
