<template>
    <b-container class="mt-20">
      <b-row class="justify-content-center">
        <b-col cols="12" md="10" lg="8">
          <div v-if="accounts.length > 0">
            <div class="summary text-center mb-4">
              <h2 class="text-light">Account Overview</h2>
              <p><strong>Total Accounts:</strong> {{ totalAccounts }}</p>
              <p><strong>Total Balance:</strong> {{ formatCurrency(totalBalance) }}</p>
              <p><strong>Average Balance:</strong> {{ formatCurrency(averageBalance) }}</p>
            </div>
  
            <b-card-group deck>
              <b-card
                v-for="account in accounts"
                :key="account.account_id"
                class="account-item"
                :title="'Account ID: ' + account.account_id"
                header-bg-variant="primary"
                text-variant="white"
                footer-bg-variant="dark"
              >
                <b-card-body>
                  <h3>{{ account.name }}</h3>
                  <p class="balance-text">{{ formatCurrency(account.balance) }}</p>
                </b-card-body>
              </b-card>
            </b-card-group>
          </div>
          <div v-else>
            <p class="text-center text-light">No accounts found.</p>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        accounts: [],
        error: null,
      };
    },
    computed: {
      totalAccounts() {
        return this.accounts.length;
      },
      totalBalance() {
        return this.accounts.reduce((acc, account) => acc + account.balance, 0);
      },
      averageBalance() {
        return this.totalBalance / this.totalAccounts || 0;
      },
    },
    methods: {
      async fetchAccounts() {
        try {
          const response = await axios.get('http://localhost:8080/account/list');
          this.accounts = response.data.data;
        } catch (error) {
          this.error = error.message || 'An error occurred';
        }
      },
      formatCurrency(value) {
        return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(value);
      },
    },
    created() {
      this.fetchAccounts();
    },
  };
  </script>
  
  <style scoped>
  .summary {
    font-weight: bold;
  }
  
  .text-center {
    text-align: center;
  }
  
  b-card-group {
    display: flex;
    flex-wrap: wrap;
    gap: 80px;
  }
  
  .account-item {
    margin-top: 20px;
    max-width: 300px;
    flex: 1;
    margin-bottom: 15px;
    transition: transform 0.2s ease-in-out;
    border-radius: 10px;
  }
  
  .account-item:hover {
    transform: scale(1.05);
  }
  
  .balance-text {
    font-size: 1.25em;
    color: #d5b608; /* Gold color for balance */
    font-weight: bold;
  }
  
  p {
    margin: 0;
  }
  </style>
  