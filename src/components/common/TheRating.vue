<script setup lang="ts">
import { ref } from 'vue'

const ratingValue = ref<Number>(0)
</script>
<template>
  <div class="rating">
    <span v-for="(n, index) in 5" :key="index">
      <input type="radio" :id="`val${index + 1}`" :value="index + 1" v-model="ratingValue" />
      <label :for="`val${index + 1}`"
        ><i
          :class="index + 1 > parseInt(ratingValue.toString()) ? 'ri-star-line' : 'ri-star-fill'"
        ></i
      ></label>
    </span>
  </div>
</template>
