<script setup>
    import Dishes_list from './components/Dishes_list.vue';
    import ModalAddDish from './components/ModalAddDish.vue';
    import Landing from './components/Landing.vue';

    const dishes = [];
    const appendDish = (dish) => {
        dishes.push(dish);
        console.log(dishes)
    }
</script>

<template>
    <Landing />
    <ModalAddDish :appendDish="appendDish" />
    <Dishes_list/>
</template>

<style scoped>

</style>
