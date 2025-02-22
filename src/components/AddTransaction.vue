<template>
    <form @submit.prevent="submitTransaction" class="mb-3">
      <div class="mb-2">
        <input v-model="title" type="text" class="form-control" placeholder="Title" required />
      </div>
      <div class="mb-2">
        <input v-model.number="amount" type="number" class="form-control" placeholder="Amount" required min="1" />
      </div>
      <div class="mb-2">
        <select v-model="type" class="form-select">
          <option value="Income">Income</option>
          <option value="Expense">Expense</option>
        </select>
      </div>
      <button type="submit" class="btn btn-primary w-100">Add</button>
    </form>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    emits: ['add-transaction'],
    setup(_, { emit }) {
      const title = ref('');
      const amount = ref(0);
      const type = ref('Income');
  
      const submitTransaction = () => {
        if (amount.value > 0) {
          emit('add-transaction', { title: title.value, amount: amount.value, type: type.value });
          title.value = '';
          amount.value = 0;
          type.value = 'Income';
        }
      };
  
      return { title, amount, type, submitTransaction };
    }
  };
  </script>
  