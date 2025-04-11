<template>
  <div class="application">
    <h2>Подача заявки</h2>
    <form @submit.prevent="submitApplication">
      <div class="form-group">
        <label>Фамилия</label>
        <input
            v-model="form.lastName"
            type="text"
            required
            placeholder="Иванов"
        />
      </div>
      <div class="form-group">
        <label>Имя</label>
        <input
            v-model="form.firstName"
            type="text"
            required
            placeholder="Иван"
        />
      </div>
      <div class="form-group">
        <label>Отчество</label>
        <input
            v-model="form.middleName"
            type="text"
            placeholder="Иванович"
        />
      </div>
      <div class="form-group">
        <label>ИНН</label>
        <input
            v-model="form.inn"
            type="text"
            pattern="\d{12}"
            required
            placeholder="123456789012"
        />
      </div>
      <div class="form-group">
        <label>Электронная почта</label>
        <input
            v-model="form.email"
            type="email"
            required
            placeholder="example@email.com"
        />
      </div>
      <div class="form-group">
        <label>Сумма кредита (₽)</label>
        <input
            v-model.number="form.loanAmount"
            type="number"
            min="10000"
            required
            placeholder="100000"
        />
      </div>
      <div v-if="isCodeSent" class="form-group">
        <label>Код подтверждения</label>
        <input
            v-model="form.verificationCode"
            type="text"
            required
            placeholder="Введите код"
        />
      </div>
      <button type="submit">
        {{ isCodeSent ? 'Подтвердить заявку' : 'Отправить заявку' }}
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'LoanApplication',
  data() {
    return {
      form: {
        lastName: '',
        firstName: '',
        middleName: '',
        inn: '',
        email: '',
        loanAmount: null,
        verificationCode: '',
      },
      isCodeSent: false,
    };
  },
  methods: {
    submitApplication() {
      if (!this.isCodeSent) {
        console.log('Отправка кода на', this.form.email);
        this.isCodeSent = true;
        alert('Код отправлен на вашу почту!');
      } else {
        console.log('Заявка отправлена:', this.form);
        alert('Заявка успешно подана!');
        this.resetForm();
      }
    },
    resetForm() {
      this.form = {
        lastName: '',
        firstName: '',
        middleName: '',
        inn: '',
        email: '',
        loanAmount: null,
        verificationCode: '',
      };
      this.isCodeSent = false;
    },
  },
};
</script>

<style scoped>
.application {
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
</style>