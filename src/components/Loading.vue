<template>
  <div
    style="
      width: 10%;
      aspect-ratio: 1/1;
      display: flex;
      justify-content: center;
      align-items: center;
      margin-inline: auto;
      margin-top: 2rem;
      color: #eb5440;
    "
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
        stroke="lightblue"
        stroke-width="2"
      />
      <path
        d="M12,4a8,8,0,0,1,7.89,6.7..."
        fill="none"
        stroke="blue"
        stroke-width="2"
      >
        <animateTransform
          attributeName="transform"
          type="rotate"
          dur="1s"
          values="0 12 12;360 12 12"
          repeatCount="indefinite"
        />
      </path>
    </svg>
  </div>
</template>
<script setup></script>
<style></style>
