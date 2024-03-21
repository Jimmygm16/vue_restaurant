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
            <h1>PJ RESTAURANT</h1>
        </div>
        <section class="manage-page">
            <Dishes_list :dishes="dishes" class="dishes_list"/>
            <ModalAddDish :appendDish="appendDish" :dishes="dishes" class="appendDish"/>
        </section>
    </div>
</template>

<style scoped>
    .manage-page {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;

        .appendDish {
            position: absolute;
            top: 58rem;
            align-items: flex-start;
            bottom: 2rem;
        }
        
    }

    .forms-container{
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    .title-container{
        display: flex;
        justify-content: center;
        padding: 4rem;
    }
</style>
