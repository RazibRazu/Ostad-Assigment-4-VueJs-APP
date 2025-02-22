<template>
  <div class="container mt-5">
    <h2 class="text-center">Expense Tracker</h2>
    <AddTransaction @add-transaction="addTransaction" />
    <TransactionList :transactions="transactions" @delete-transaction="deleteTransaction" />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import AddTransaction from './components/AddTransaction.vue';
import TransactionList from './components/TransactionList.vue';

export default {
  components: { AddTransaction, TransactionList },
  setup() {
    const transactions = ref([]);

    onMounted(() => {
      const savedTransactions = JSON.parse(localStorage.getItem('transactions')) || [];
      transactions.value = savedTransactions;
    });

    const addTransaction = (transaction) => {
      transactions.value.push(transaction);
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    };

    const deleteTransaction = (index) => {
      transactions.value.splice(index, 1);
      localStorage.setItem('transactions', JSON.stringify(transactions.value));
    };

    return { transactions, addTransaction, deleteTransaction };
  }
};
</script>

<style>
body {
  background-color: #1e1e1e;
  color: white;
}
</style>
