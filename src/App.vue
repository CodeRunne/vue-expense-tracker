<template>
  <div class="w-[20rem] p-2 my-3">
    <ExpenseHeader />
    <ExpenseBalance :total="total" />
    <IncomeExpense :incomes="+incomes" :expenses="+expenses" />
    <TransactionHistory :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>


<script setup>
  import ExpenseHeader from '@/components/ExpenseHeader.vue'
  import ExpenseBalance from '@/components/ExpenseBalance.vue'
  import IncomeExpense from '@/components/IncomeExpense.vue'
  import TransactionHistory from '@/components/TransactionHistory.vue'
  import AddTransaction from '@/components/AddTransaction.vue'

  import { ref, computed, onMounted } from 'vue'
  import { useToast} from 'vue-toastification'

  const toast = useToast()
  const transactions = ref([])

  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'))

    if(savedTransactions) {
      transactions.value = savedTransactions
    }
  })

  // Get Total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(3)
  });

  // Get Income
  const incomes = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2)
  });

  // Get Expenses
  const expenses = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2)
  });

  // Add Transaction
  const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount
    })

    savedTransactionsToLocalStorage()
    toast.success('Transaction added')
  }

  const handleTransactionDeleted = (id) => {
    console.log(id)
    transactions.value = transactions.value.filter((transaction) => transaction.id != id)
    savedTransactionsToLocalStorage()
    toast.success("Transaction Deleted")
  }

  // Generate unique id
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000000)
  }

  // Save to localstorage
  const savedTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
  }
</script>