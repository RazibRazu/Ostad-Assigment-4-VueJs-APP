<template>
    <table class="table table-dark table-striped">
      <thead>
        <tr>
          <th>Title</th>
          <th>Amount</th>
          <th>Type</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(transaction, index) in transactions" :key="index">
          <td>{{ transaction.title }}</td>
          <td :class="{ 'text-danger': transaction.amount >= 500 }">${{ transaction.amount }}</td>
          <td :class="transaction.type === 'Income' ? 'text-success' : 'text-danger'">{{ transaction.type.toUpperCase() }}</td>
          <td>
            <button @click="$emit('delete-transaction', index)" class="btn btn-danger btn-sm">Delete</button>
          </td>
        </tr>
        <tr v-if="transactions.length === 0">
          <td colspan="4" class="text-center">No transactions recorded yet.</td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script>
  export default {
    props: ['transactions']
  };
  </script>
  