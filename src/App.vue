<script setup>
    import ModalAddDish from './components/ModalAddDish.vue';
    import Landing from './components/Landing.vue';

    const dishes = [];
    const appendDish = (dish) => {
        dishes.push(dish);
        console.log(dishes)
    }

</script>

<template>
  <div class="page-content">
    <Landing />
    <ModalAddDish :appendDish="appendDish" />
  </div>
</template>

<style scoped>
  .page-content {
    margin: 0;
    padding: 0;
  }
</style>
