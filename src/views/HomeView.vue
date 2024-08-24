<script setup lang="ts">
import { ref } from 'vue'
import KanbanList from '@/components/home/KanbanList.vue'

interface taskType {
  id: number
  title: String
}
const todoItems = ref<Array<taskType>>([
  { id: 1, title: 'Designing' },
  { id: 2, title: 'Development' },
  { id: 3, title: 'Testing' }
])

const inProgressItems = ref<Array<taskType>>([])

const doneItems = ref<Array<taskType>>([])

const draggedItem = ref()
const draggedItemType = ref()

const storeDraggedItem = (item: object, id: String) => {
  draggedItem.value = item
  draggedItemType.value = id
  console.log(draggedItem.value, draggedItemType.value)
}
const removeItemFromList = (listName: String) => {
  switch (listName) {
    case 'todo':
      todoItems.value = todoItems.value.filter((item) => item.id !== draggedItem.value.id)
      break
    case 'inProgress':
      inProgressItems.value = inProgressItems.value.filter(
        (item) => item.id !== draggedItem.value.id
      )
      break
    case 'done':
      doneItems.value = doneItems.value.filter((item) => item.id !== draggedItem.value.id)
      break
  }
}

const addItemToList = (listName: String) => {
  switch (listName) {
    case 'todo':
      todoItems.value.push(draggedItem.value)
      break
    case 'inProgress':
      inProgressItems.value.push(draggedItem.value)
      break
    case 'done':
      doneItems.value.push(draggedItem.value)
      break
  }
}
const filterTaskList = (dropToId: String) => {
  // console.log(dropToId, draggedItem.value.id)
  removeItemFromList(draggedItemType.value)
  addItemToList(dropToId)
}

const addNewItem = (info: object) => {
  console.log('add new item ', info)
  let item = { id: Number(info.newTaskId), title: info.newTask }
  draggedItem.value = item
  console.log(item)
  addItemToList(info.id)
  // draggedItemType.value = id
}
</script>

<template>
  <main>
    <div class="container py-5">
      <h2 class="text-center mb-4">Kanban Board</h2>
      <div class="row">
        <!-- To Do Column -->
        <div class="col-lg-4">
          <KanbanList
            title="To Do"
            :items="todoItems"
            id="todo"
            @filter-task="filterTaskList"
            @drag-event="storeDraggedItem"
            @add-item-to-list="addNewItem"
          />
        </div>
        <!-- In Progress Column -->
        <div class="col-lg-4">
          <KanbanList
            title="In Progress"
            :items="inProgressItems"
            id="inProgress"
            @filter-task="filterTaskList"
            @drag-event="storeDraggedItem"
            @add-item-to-list="addNewItem"
          />
        </div>
        <!-- Done Column -->
        <div class="col-lg-4">
          <KanbanList
            title="Done"
            :items="doneItems"
            id="done"
            @filter-task="filterTaskList"
            @drag-event="storeDraggedItem"
            @add-item-to-list="addNewItem"
          />
        </div>
      </div>
    </div>
  </main>
</template>
