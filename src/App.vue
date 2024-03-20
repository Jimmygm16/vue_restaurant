<script setup>
    import Dishes_list from './components/Dishes_list.vue';
    import ModalAddDish from './components/ModalAddDish.vue';
    import Landing from './components/Landing.vue';
    import { ref } from 'vue';

    const dishes = ref([]);
    const appendDish = (dish) => {
        dishes.value.push(dish);
    }
</script>

<template>
    <Landing />
    <section class="manage-page">
      <Dishes_list :dishes="dishes" class="dishes_list"/>
      <ModalAddDish :appendDish="appendDish" />
    </section>
</template>

<style scoped>
    .manage-page {
        display: flex;
        height: 100vh;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        .appendDish {
            margin-right: 9.5rem; 
            align-items: flex-start;
            position: relative;
            bottom: 2rem;
        }
        
    }
</style>
