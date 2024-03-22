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
    <div class="forms-container">
        <div class="title-container">
            <h1>PJ RESTAURANT 🧆</h1>
            <ModalAddDish :appendDish="appendDish" :dishes="dishes" class="appendDish"/>
        </div>
        <section class="manage-page">
            <Dishes_list :dishes="dishes" class="dishes_list"/>
        </section>
    </div>
</template>

<style scoped>
    .manage-page {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        /* .appendDish {
            position: relative;
            top: -9rem;
            right: 0.5rem;
            align-items: flex-start;
            bottom: 2rem;
        }
         */
    }

    .forms-container{
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    .title-container{
        display: flex;
        justify-content: space-between;
        margin: 4rem 3rem 0.5rem 3rem;
        border-bottom: solid 0.1rem var(--light-slate-gray);
    }
</style>
