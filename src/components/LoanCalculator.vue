<template>
  <div class="calculator">
    <h2>Калькулятор кредита</h2>
    <div class="form-group">
      <label>Сумма кредита (₽)</label>
      <input
          v-model.number="amount"
          type="number"
          min="10000"
          max="1000000"
          placeholder="Введите сумму"
      />
    </div>
    <div class="form-group">
      <label>Срок кредита (месяцев)</label>
      <input
          v-model.number="term"
          type="number"
          min="1"
          max="60"
          placeholder="Введите срок"
      />
    </div>
    <div class="form-group">
      <label>Процентная ставка (%)</label>
      <input
          v-model.number="rate"
          type="number"
          min="1"
          max="30"
          step="0.1"
          placeholder="Введите ставку"
      />
    </div>
    <button @click="calculate">Рассчитать</button>
    <div v-if="result" class="result">
      <p>Ежемесячный платеж: <strong>{{ result.monthlyPayment }} ₽</strong></p>
      <p>Общая переплата: <strong>{{ result.totalInterest }} ₽</strong></p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoanCalculator',
  data() {
    return {
      amount: 100000,
      term: 12,
      rate: 10,
      result: null,
    };
  },
  methods: {
    calculate() {
      const principal = this.amount;
      const monthlyRate = this.rate / 100 / 12;
      const numberOfPayments = this.term;

      // Аннуитетный платеж
      const monthlyPayment =
          (principal * monthlyRate) /
          (1 - Math.pow(1 + monthlyRate, -numberOfPayments));
      const totalPaid = monthlyPayment * numberOfPayments;
      const totalInterest = totalPaid - principal;

      this.result = {
        monthlyPayment: monthlyPayment.toFixed(2),
        totalInterest: totalInterest.toFixed(2),
      };
    },
  },
};
</script>

<style scoped>
.calculator {
  background-color: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h2 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.form-group {
  margin-bottom: 1rem;
}

label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  margin-bottom: 0.25rem;
}

input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #d1d5db;
  border-radius: 0.25rem;
  font-size: 1rem;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

button {
  width: 100%;
  background-color: #2563eb;
  color: white;
  padding: 0.75rem;
  border: none;
  border-radius: 0.25rem;
  font-size: 1rem;
  cursor: pointer;
}

button:hover {
  background-color: #1d4ed8;
}

.result {
  margin-top: 1rem;
  text-align: center;
}

.result p {
  font-size: 1rem;
  margin-bottom: 0.5rem;
}

.result strong {
  font-weight: 600;
}
</style>