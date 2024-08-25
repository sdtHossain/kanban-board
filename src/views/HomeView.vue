<script setup lang="ts">
import { ref } from 'vue'
import KanbanList from '@/components/home/KanbanList.vue'

interface taskType {
  id: number
  title: String
}
interface emitItemType {
  item?: taskType
  index: number
  id: String
}
const todoItems = ref<Array<taskType>>([
  { id: 1, title: 'Designing' },
  { id: 2, title: 'Development' },
  { id: 3, title: 'Testing' }
])

const inProgressItems = ref<Array<taskType>>([
  { id: 1, title: 'revise' },
  { id: 2, title: 'polish' },
  { id: 3, title: 'deploy' }
])

const doneItems = ref<Array<taskType>>([])

const draggedItem = ref<taskType | null>()
const draggedItemIndex = ref<number | null>()
const draggedItemTaskType = ref<String | null>()

// functions
const removeItemFromList = (listName: String) => {
  switch (listName) {
    case 'todo':
      todoItems.value = todoItems.value.filter((item) => item.title !== draggedItem.value!.title)
      break
    case 'inProgress':
      inProgressItems.value = inProgressItems.value.filter(
        (item) => item.title !== draggedItem.value!.title
      )
      break
    case 'done':
      doneItems.value = doneItems.value.filter((item) => item.title !== draggedItem.value!.title)
      break
  }
}
const addItemToList = (listName: String) => {
  switch (listName) {
    case 'todo':
      todoItems.value.push(draggedItem.value!)
      break
    case 'inProgress':
      inProgressItems.value.push(draggedItem.value!)
      break
    case 'done':
      doneItems.value.push(draggedItem.value!)
      break
  }
}

const moveItemWithinList = (listName: String, newIndex: number) => {
  let temp
  switch (listName) {
    case 'todo':
      temp = todoItems.value.splice(draggedItemIndex.value!, 1)[0]
      todoItems.value.splice(newIndex, 0, temp)
      draggedItemIndex.value = newIndex
      break
    case 'inProgress':
      temp = inProgressItems.value.splice(draggedItemIndex.value!, 1)[0]
      inProgressItems.value.splice(newIndex, 0, temp)
      draggedItemIndex.value = newIndex
      break
    case 'done':
      temp = doneItems.value.splice(draggedItemIndex.value!, 1)[0]
      doneItems.value.splice(newIndex, 0, temp)
      draggedItemIndex.value = newIndex
      break
  }
}

const addItemToListInDedicatedIndex = (listName: String, indexAddTo: number) => {
  switch (listName) {
    case 'todo':
      todoItems.value.splice(indexAddTo, 0, draggedItem.value)
      break
    case 'inProgress':
      inProgressItems.value.splice(indexAddTo, 0, draggedItem.value)
      break
    case 'done':
      doneItems.value.splice(indexAddTo, 0, draggedItem.value)
      break
  }
}

// ------------- //

const onDragStart = (info: emitItemType) => {
  draggedItem.value = info.item
  draggedItemIndex.value = info.index
  draggedItemTaskType.value = info.id
}

const onDrop = (e: DragEvent, info: emitItemType) => {
  e.preventDefault()
  // draggedItem.value = null
  // draggedItemIndex.value = null
  // draggedItemTaskType.value = null
  if (draggedItemTaskType.value == info.id && draggedItemIndex.value !== info.index) {
    moveItemWithinList(info.id, info.index)
  } else if (draggedItemTaskType.value !== info.id) {
    removeItemFromList(draggedItemTaskType.value!)
    addItemToListInDedicatedIndex(info.id, info.index)
  }
}

const onDragEnd = () => {
  draggedItem.value = null
  draggedItemIndex.value = null
  draggedItemTaskType.value = null
}

const onDropToColumn = (id: String) => {
  if (draggedItemTaskType.value !== id) {
    removeItemFromList(draggedItemTaskType.value!)
    addItemToList(id)
  }
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
            @on-drag-start-event="onDragStart"
            @on-drop-event="onDrop"
            @on-drag-end-event="onDragEnd"
            @in-drop-to-column="onDropToColumn"
          />
        </div>
        <!-- In Progress Column -->
        <div class="col-lg-4">
          <KanbanList
            title="In Progress"
            :items="inProgressItems"
            id="inProgress"
            @on-drag-start-event="onDragStart"
            @on-drop-event="onDrop"
            @on-drag-end-event="onDragEnd"
            @in-drop-to-column="onDropToColumn"
          />
        </div>
        <!-- Done Column -->
        <div class="col-lg-4">
          <KanbanList
            title="Done"
            :items="doneItems"
            id="done"
            @on-drag-start-event="onDragStart"
            @on-drop-event="onDrop"
            @on-drag-end-event="onDragEnd"
            @in-drop-to-column="onDropToColumn"
          />
        </div>
      </div>
    </div>
  </main>
</template>
