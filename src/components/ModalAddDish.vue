<template>
    <section>
        <button class="modal-button" @click="openModal = true">
            <span>
                Añadir plato!
            </span> 
        </button>
        <transition name="fade" appear>
            <div class="modal-overlay" v-if="openModal" @click="openModal = false">
            </div>
        </transition>
        <transition name="fade" appear>
            <div class="modal-content" v-if="openModal">
                <h3 class="modal-tittle">
                    Añade tu nuevo plato!
                </h3>
                <form class="modal-form" action="">
                    <input @input="onChangeInput" name="name" type="text" placeholder="Nombre del plato" required>
                    <input @input="onChangeInput" name="price" type="number" placeholder="Costo del plato" required>
                    <button class="modal-form-button" @click="addNewDish">
                        Añadir plato
                    </button>
                </form>
            </div>
        </transition>
    </section>
</template>

<script>
    import { ref } from 'vue';

    export default {
        data() {
            return {
                openModal: false
            }
        },
        props: {
            appendDish: {
                type: Function,
                required: true
            }
        },
        setup(props) {
            const openModal = ref(false);
            let dish = {
                name: '',
                price: 0,
                paid: 0,
                gifted: 0
            }

            const addNewDish = (event) => {
                if (!dish.name || !dish.price) {
                    return;
                }

                event.preventDefault();
                props.appendDish(dish);

                dish = {
                    name: '',
                    price: 0,
                    paid: 0,
                    gifted: 0
                }

                openModal.value = false;
            }

            const onChangeInput = (event) => {
                if (event.target.name === 'price') {
                    dish[event.target.name] = parseFloat(event.target.value);
                } else {
                    dish[event.target.name] = event.target.value;
                }
            }

            return {
                openModal,
                dish,
                addNewDish,
                onChangeInput,
            }
        }
    }
</script>

<style scoped>
    .modal-button,
    .modal-form-button {
        background-color: #899FB6;
        color: white;
        padding: 0.4rem 1rem;
        border-radius: 6px;
        border: none;
        font-size: medium;
        transition: background-color 0.3s;
    }

    .modal-button:hover,
    .modal-form-button:hover {
        background-color: #425164;
        cursor: pointer;
        box-shadow: rgba(0, 0, 0, 0.2);
    }

    .modal-overlay {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 1;
        background-color: rgba(0, 0, 0, 0.2);
    }

    .fade-enter-active,
    .fade-leave-active {
        transition: opacity 0.5s;
    }

    .fade-enter,
    .fade-leave-to {
        opacity: 0;
    }

    .modal-content {
        display: flex;
        flex-direction: column;

        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: #FFF;
        border-radius: 10px;
        padding: 2rem;
        z-index: 10;

        .modal-tittle {
            margin: 0;
            padding: 0 0 1.5rem 0;
        }

        .modal-form {
            display: flex;
            flex-direction: column;
            grid-gap: 0.7rem;

            button {
                width: fit-content;
                margin-top: 1.2rem;
            }

            input, textarea {
                padding: 0.5rem 0.8rem;
                border-radius: 10px;
                border: none;
                background-color: #EEE;
                transition: border-color 0.3s;
            }
        }
    }
</style>
