<script>
    import { ref, watch } from 'vue';

    export default {
        props: {
            showModal: {
                type: Boolean,
                default: false
            },
            dishAdded:{
                type: Boolean,
                default: false
            }
        },
        setup(props, { emit }) {
            const internalShowModal = ref(props.showModal);
            const internalDishAdded = ref(props.dishAdded)
            const paidDishes = ref(0)
            const giftedDishes = ref(0)

            const closeModal = () => {
                internalShowModal.value = false;
                emit('update:showModal', false);
            };

            const changeDishStatus = () =>{
                emit('update:dishAdded', true);
                emit('addDish', {paid: paidDishes.value, gifted: giftedDishes.value});
                closeModal();
                paidDishes.value = 0
                giftedDishes.value = 0
            }

            watch(
                () => props.showModal,
                () => { internalShowModal.value = props.showModal; }
            );

            watch(
                () => props.dishAdded,
                () => { internalDishAdded.value = props.dishAdded; }
            );

            return {
                closeModal,
                changeDishStatus,
                internalShowModal,
                paidDishes,
                giftedDishes
            };
        }
    }
</script>

<template>
    <div v-if="internalShowModal" class="modal-wrapper">
        <div class="modal">
            <div class="icon-container">
                <img class="icon-x" src="../assets/cross.png" @click="closeModal"/>
            </div>
            <h2 class="modal-title">Add a dish!</h2>
            <div class="modal-form">
                <div class="input-wrapper">
                    <input type="number" v-model="paidDishes" placeholder=" " class="floating-input">
                    <label class="placeholder">PAID DISHES</label>
                </div>
                <div class="input-wrapper">
                    <input type="number" v-model="giftedDishes" placeholder=" " class="floating-input">
                    <label class="placeholder">GIFTED DISHES</label>
                </div>
            </div>
            <div class="button-container">
                <button @click="changeDishStatus()">Add</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .input-wrapper {
        position: relative;
        margin-bottom: 1rem;
    }

    .floating-input {
        border: none;
        border-bottom: solid 0.1rem var(--light-slate-gray);
        transition: border-color 0.5s;
        width: 100%;
        padding-bottom: 0.5rem;
    }

    .floating-input:focus {
        outline: none;
        border-bottom-color: #333;
        transition: border-color 0.5s;
    }

    .placeholder {
        position: absolute;
        bottom: 0.5rem;
        left: 0;
        transition: all 0.3s;
        pointer-events: none; 
        color: #777;
    }

    .floating-input:focus + .placeholder,
    .floating-input:not(:placeholder-shown) + .placeholder {
        bottom: 100%;
        font-size: 0.8rem;
        color: #333;
    }

    .modal {
        border: solid 0.1rem var(--light-slate-gray);
        border-radius: 0.5rem;
        background-color: white;
        padding: 1rem;
        max-width: 20rem;
        max-height: fit-content;
    }

    .modal-wrapper {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        justify-content: center; 
        align-items: center; 
        z-index: 9999; 
    }

    .modal-form {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    .modal-title {
        text-align: center;
        text-transform: uppercase;
        margin-bottom: 2.5rem;
    }

    .icon-container{
        display: flex;
        justify-content: end;
    }

    .icon-container:hover{
        cursor: pointer;
    }

    .icon-x{
        width: 1rem;
        height: 1rem;
    }

    .button-container{
        display: flex;
        justify-content: center;
    }


</style>