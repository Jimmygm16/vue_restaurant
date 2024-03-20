<script>
import { ref } from 'vue';
import Modal from './Modal.vue'

export default {
    props: {
        dishes: {
            type: Array,
            required: true
        }
    },
    components: {
        Modal
    },
    setup(props) {
        const areDishesToPay = ref(false)

        const actualIndex = ref(-1);
        const dishAdded = ref(false);
        const dishesToPay = ref([]);
        const totalToPaid = ref(0)

        const showModal = ref(false);

        const openModal = (key) => {
            showModal.value = true;
            actualIndex.value = key;
        };

        const deleteDish = (index)=>{
            dishesToPay.value.splice(index, 1);
            dishesToPay.value.length > 0 ? areDishesToPay.value = true : areDishesToPay.value = false;
            calculateTotalToPay();
        }

        const calculateTotalToPay = ()=>{
            totalToPaid.value = dishesToPay.value.reduce(function (result, item){
                return result + (item.paid * item.price);
            }, 0)
        }

        const showCurrency = (value) => {
            try {
                const formatter = new Intl.NumberFormat('es-CO', {
                style: 'currency',
                currency: 'COP',
                minimumFractionDigits: 0,
                });
                return formatter.format(value);
            } catch (error) {
                return `COP ${value.toFixed(2)}`; 
            }
        }

        const addDish = (dishData) => {
            if (dishAdded.value && actualIndex.value !== -1 && (dishData.paid > 0 || dishData.gifted > 0)){
                const dishToPay = props.dishes[actualIndex.value];
                const existingIndex = dishesToPay.value.findIndex(item => item.name === dishToPay.name);
                if (existingIndex === -1) {
                    dishToPay.paid = dishData.paid;
                    dishToPay.gifted = dishData.gifted; 
                    dishesToPay.value.push(dishToPay);
                    dishesToPay.value.length > 0 ? areDishesToPay.value = true : areDishesToPay.value = false;
                    dishAdded.value = false;
                    calculateTotalToPay();
                };
            }
            dishesToPay.value.length > 0 ? areDishesToPay.value = true : areDishesToPay.value = false;
            dishAdded.value = false;
        }

        return {
            showModal,
            dishAdded,
            dishesToPay,
            areDishesToPay,
            totalToPaid,
            openModal,
            addDish,
            deleteDish,
            calculateTotalToPay,
            showCurrency
        };
    }
}
</script>

<template>
    <div class="dishes-result">
        <div>
            <table>
                <tr>
                    <th>Dish name</th>
                    <th>Price</th>
                </tr>
                <tr v-for="(dish, index) in dishes" :key="index">
                    <td>{{ dish.name }}</td>
                    <td>{{ showCurrency(dish.price) }}</td>
                    <td>
                        <img class="icon-add" src="../assets/plus.png" @click="openModal(index)" />
                    </td>
                </tr>
            </table>
        </div>
        <div class="main-content">
            <table v-if="areDishesToPay && totalToPaid > 0">
                <tr>
                    <th>Dish name</th>
                    <th>Price</th>
                    <th>Quantity</th>
                    <th>Total</th>
                </tr>
                <tr v-for="(dishToPay, index) in dishesToPay" :key="index">
                    <td>{{ dishToPay.name }}</td>
                    <td>{{ showCurrency(dishToPay.price) }}</td>
                    <td>{{ dishToPay.gifted + dishToPay.paid}}</td>
                    <td>{{ showCurrency(dishToPay.paid * dishToPay.price) }}</td>
                    <td> <img class="icon-add" src="../assets/delete.png" @click="deleteDish(index)" /></td>
                </tr>
                <tr>
                    <td><b>Total</b></td>
                    <td></td>
                    <td></td>
                    <td>{{ showCurrency(totalToPaid) }}</td>
                    <td></td>
                </tr>
            </table>
            <div v-else-if="totalToPaid == 0" class="content-message">
                <h1>There is nothing to pay!</h1>
            </div>
        </div>
    </div>
    <Modal v-model:showModal="showModal" v-model:dishAdded="dishAdded" @addDish="addDish" />
</template>

<style scoped>

    table {
        border-collapse: collapse;
        width: 100%;
    }

    tr:nth-child(even) {
        background-color: var(--tan);
    }

    tr {
        border: solid 0.1rem var(--tan);
        padding: 0.5rem;
        text-align: left;
    }

    td, th {
        padding: 0.8rem;
        text-align: center;
    }

    .icon-add{
        width: 1.5rem;
        height: 1.5rem;
    }

    .icon-add:hover{
        cursor: pointer;
    }

    .content-message{
        border: solid 0.1rem var(--light-slate-gray);
        width: fit-content;
        border-radius: 0.8rem;
        padding: 1rem;
        background-color: var(--tan);
    }

    .main-content{
        display: grid;
        grid-template-columns: repeat(1, 1fr);
        width: 100%;
    }

    .dishes-result{
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        padding: 3rem;
        gap: 2rem;
    }

</style>
