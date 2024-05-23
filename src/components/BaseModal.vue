<template>
    <div class="modal" v-if="isOpen">
      <div class="modal-content">
        <span class="close" @click="$emit('close')">&times;</span>
        <slot></slot>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['isOpen'],
  };
  </script>
  
  <style scoped>
  .modal {
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
  }
  
  .modal-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    width: 80%;
    max-width: 500px;
    position: relative;
  }
  
  .close {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 1.5rem;
    cursor: pointer;
  }
  </style>
  