<script setup lang="ts">
import TheBanner from '@/components/home/TheBanner.vue'
</script>

<template>
  <main>
    <div class="container py-5">
      <h2 class="text-center mb-4">Kanban Board</h2>
      <div class="row">
        <!-- To Do Column -->
        <div class="col-lg-4">
          <div class="kanban-column">
            <div class="kanban-header">To Do</div>
            <div class="kanban-item">Task 1: Research</div>
            <div class="kanban-item">Task 2: Planning</div>
            <div class="kanban-item">Task 3: Design</div>
          </div>
        </div>
        <!-- In Progress Column -->
        <div class="col-lg-4">
          <div class="kanban-column">
            <div class="kanban-header">In Progress</div>
            <div class="kanban-item">Task 4: Development</div>
            <div class="kanban-item">Task 5: Testing</div>
          </div>
        </div>
        <!-- Done Column -->
        <div class="col-lg-4">
          <div class="kanban-column">
            <div class="kanban-header">Done</div>
            <div class="kanban-item">Task 6: Review</div>
            <div class="kanban-item">Task 7: Deployment</div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
