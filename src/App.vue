<script setup>
    import ModalAddDish from './components/ModalAddDish.vue';

    const dishes = [];
    const appendDish = (dish) => {
        console.log(dish);
    }

</script>

<template>
  <div>
    <ModalAddDish :appendDish="appendDish" />
  </div>
</template>

<style scoped>

</style>
