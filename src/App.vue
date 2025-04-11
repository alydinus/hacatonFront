<template>
  <div class="wrapper">
    <header class="header">
      <div class="container">
        <h1>Сервис кредитования</h1>
        <p>Рассчитайте и подайте заявку на кредит</p>
      </div>
    </header>
    <main class="main">
      <div class="grid">
        <LoanCalculator />
        <LoanApplication />
      </div>
    </main>
  </div>
</template>

<script>
import LoanCalculator from './components/LoanCalculator.vue';
import LoanApplication from './components/LoanApplication.vue';

export default {
  name: 'App',
  components: {
    LoanCalculator,
    LoanApplication,
  },
};
</script>

<style scoped>
.wrapper {
  min-height: 100vh;
  background-color: #f3f4f6;
}

.header {
  background-color: #2563eb;
  color: white;
  padding: 1.5rem 0;
  text-align: center;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.header h1 {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.header p {
  font-size: 1rem;
}

.main {
  padding: 2.5rem 0;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: 1fr 1fr;
  }
}

</style>