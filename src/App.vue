<template>
  <div id="app">
    <div class="hero-section">
      <h1 class="hero-title text-center">Your Financial Dashboard</h1>
      <AccountList />
    </div>
  </div>
</template>

<script>
import AccountList from './components/accountList.vue';

export default {
  name: 'App',
  components: {
    AccountList
  }
};
</script>

<style>
/* Global styles for the app */
#app {
  background-color: #4e5155; /* Light gray background */
  color: #333333; /* Dark text color for readability */
  min-height: 100vh; /* Full viewport height */
  padding: 40px 20px;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Roboto', sans-serif;
}

.hero-section {
  text-align: center;
  padding: 30px 40px;
  border-radius: 10px;
  background-color: #ffffff; /* White background for the content */
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  max-width: 1200px;
  width: 100%;
}

.hero-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 20px;
  color: #003366;
}

@media (max-width: 768px) {
  /* Responsiveness for smaller screens */
  .hero-title {
    font-size: 2rem;
  }

  .hero-section {
    padding: 20px 25px;
  }
}
</style>
