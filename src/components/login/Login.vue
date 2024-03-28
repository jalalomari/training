<template>
  <div class="mx-auto my-10 w-50">
    <div class="p-12 border border-gray-200 bg-white">
      <!-- form input binding v-model / template refs-->
      <form ref="loginForm" @submit.prevent="login" v-bind="$attrs">
        <div class="text-left mb-0">
          <PropsLogin pageTitle="Login" pageDescription="Welcome" />  <!-- Props -->
        </div>
        <div class="fv-row mb-7">
          <label for="email" class="form-label fs-6 fw-normal text-dark">Email</label>
          <input v-model="username" id="email" type="email" autocomplete="off"
            class="form-control bg-white form-control-lg min-h-sm-45px min-h-35px"
            :class="{ 'border-danger': errors.username }" />
            <label v-if="showInputLabel" class="text-sm text-gray-500">Typing...</label>
          <div class="mt-1 text-red-500 text-sm text-danger">{{ errors.username }}</div>
        </div>
        <div class="fv-row mb-7">
          <div class="d-flex flex-stack mb-2">
            <label for="password" class="form-label fw-normal text-dark fs-6 mb-0">Password</label>
          </div>
          <input v-model="password" id="password" class="form-control bg-white min-h-sm-45px min-h-35px form-control-lg"
            type="password" name="password" autocomplete="off" 
            :class="{ 'border-danger': errors.password }" />
          <div class="mt-1 text-red-500 text-sm text-danger">{{ errors.password }}</div>
        </div>
        <div v-if="errorMessage" class="alert alert-danger mt-3" role="alert">
          {{ errorMessage }}
        </div>
        <ButtonTemp v-bind="$attrs" :disabled="!username.trim() || !password.trim()">  <!-- Attribute --> 
          Sign In <!-- slot content -->
        </ButtonTemp>

      </form>
    </div>
  </div>
</template>
<script setup>
import Swal from 'sweetalert2';
import { ref, onMounted, watch, watchEffect, defineEmits } from 'vue';
import { useRouter } from 'vue-router';
import PropsLogin from '@/views/PropsLogin.vue';
import ButtonTemp from '@/components/buttons/Button.vue';

const router = useRouter(); 
const loginForm = ref(null);
const username = ref('');
const password = ref('');
const errors = ref({ username: '', password: '' });
const errorMessage = ref('');
const showInputLabel = ref(false);

// events emit
const emits = defineEmits(['loginSuccess']);

// lifecycle hook: mounted
onMounted(() => {
  console.log('Login Form:', loginForm.value);
});

// watchers
watch([username, password], ([newUsername, newPassword], [oldUsername, oldPassword]) => {
  console.log('Username changed from', oldUsername, 'to', newUsername);
  console.log('Password changed from', oldPassword, 'to', newPassword);
});
watchEffect(() => {
  if (username.value.length > 0) {
    showInputLabel.value = true;
    const timer = setTimeout(() => {
      showInputLabel.value = false;
    }, 1000);
    return () => clearTimeout(timer);
  }
});

//form validation - Promise(resolve, reject)
function login() {
  return new Promise((resolve, reject) => {
    clearErrors();
    if (!username.value.trim()) {
      errors.value.username = 'The email field is required';
      reject(errors.value.username);
      return; 
    }
    if (!password.value.trim()) {
      errors.value.password = 'The password field is required';
      reject(errors.value.password);
      return; 
    }
    if (password.value.trim().length < 6) {
      errors.value.password = 'The password must be at least 6 characters';
      reject(errors.value.password);
      return; 
    }
    fetch('https://4d00e099-79e7-49c2-95db-db717a3a036f.mock.pstmn.io/api/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        username: username.value,
        password: password.value
      })
    })
    .then(response => {
      if (!response.ok) {
        throw new Error('Failed to login. Please try again later.');
      }
      return response.json();
    })
    .then(data => {
      if (data.username === username.value && data.password === password.value) {
        showSuccessAlert('Logged in successfully');
        // Emit
        emits('loginSuccess');
        router.push('/home');
        resolve(data);
      } else {
        showErrorAlert('Invalid credentials');
        reject('Invalid credentials');
      }
    })
    .catch(error => {
      showErrorAlert(error.message || 'Failed to login. Please try again later.');
      reject(error);
    });
  })
  .catch(error => {
    showErrorAlert(error.message || 'Failed to login. Please try again later.');
  });
}
function clearErrors() {
  errors.value = { username: '', password: '' };
  errorMessage.value = '';
}
// simulated server-side validation
// function simulatedLoginApi(username, password) {
//   return new Promise((resolve) => {
//     if (username === 'demo@example.com' && password === 'demo123') {
//       resolve({ data: true });
//     } else {
//       resolve({ data: false });
//     }
//   });
// }
//event handling
function showSuccessAlert(message) { 
  Swal.fire({ toast: true, timer: 1000, position: 'top-end', timerProgressBar: true, title: message, icon: 'success', showConfirmButton: false, showCloseButton: true });
}
function showErrorAlert(message) { 
  Swal.fire({ title: message, icon: 'error', customClass: { confirmButton: 'btn btn-primary' } });
}
</script>