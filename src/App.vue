
<template>
    <Header/>
    <div class="container">
        <Balance :total="total" />
        <IncomeExpenses :income='income' :expenses='expenses' />
        <TransactionList :transactions="transactions" />
        <AddTransaction />
    </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';
    
import {ref, computed} from 'vue';

const transactions = ref([
    {id:1, text: 'flower', amount: -19.99 },
    {id:2, text: 'salary', amount: 299.99 },
    {id:3, text: 'Book', amount: -20 },
    {id:4, text: 'Camera', amount: 119.99 },
]);

const total = computed(() => {
    return transactions.value.reduce((acc, transaction)=>{
        return acc + transaction.amount;
    }, 0);
});

// get income
const income = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction)=>{
        return acc + transaction.amount;
    }, 0).toFixed(2);
});

// get expenses
const expenses = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0 )
    .reduce((acc, transaction)=>{
        return acc + transaction.amount;
    }, 0).toFixed(2);
});
</script>