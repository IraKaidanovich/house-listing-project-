<template>
  <div
    v-show="isVisible"
    class="spinner-container"
  >
    <div
      class="spinner"
    >
      <svg
        width="100%"
        height="100%"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M12,4a8,8,0,0,1,7.89,6.7..."
          fill="none"
          stroke="#b1564a"
          stroke-width="2"
        />
        <path
          d="M12,4a8,8,0,0,1,7.89,6.7..."
          fill="none"
          stroke="#eb5440"
          stroke-width="2"
        >
          <animateTransform
            attributeName="transform"
            type="rotate"
            dur="0.5s"
            values="0 12 12;360 12 12"
            repeatCount="indefinite"
          />
        </path>
      </svg>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const isVisible = ref(true);

setTimeout(() => {
  isVisible.value = false;
}, 3000);
</script>

<style>
.spinner-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #fff;
  transition: opacity 1s ease-out; 
  opacity: 1; 
}

.spinner-container[v-show="false"] {
  opacity: 0;
  pointer-events: none; 
}

.spinner {
  width: 10%;
  aspect-ratio: 1/1;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

