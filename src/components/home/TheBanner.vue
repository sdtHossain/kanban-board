<script setup lang="ts">
import { ref } from 'vue'
import TheRating from '../common/TheRating.vue'
</script>
<template>
  <div class="bg-gray home-banner">
    <div class="container" style="min-height: 600px">
      <div class="row">
        <div class="col-lg-6">
          <h1 class="display-5 fw-bold py-5">Responsive left-aligned hero with image</h1>

          <div class="bg-gray">
            <TheRating />
            <span>Based on Customer Review</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
