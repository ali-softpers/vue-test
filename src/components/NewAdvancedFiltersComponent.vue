<template>
   <button @click="showModal = true" class="button">Show Modal</button>

    <div class="modal-overlay" 
         @click="showModal = false"></div>
  
    <div class="modal" 
         role="dialog" 
         
         >
      <h1>Vue Transitions</h1>
      <p>The <code>&lt;transition&gt;</code> component in Vue can create wonderful animated entrances and exits.</p>
      <button @click="showModal = false" class="button">Hide Modal</button>

    </div>
  
</template>

<script>
  export default {
  
  data() {
    return {
      allJson: this.all,
      showModal: true
  }}}
</script>