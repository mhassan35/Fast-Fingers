<template>
  <div v-if="dialog" class="modal-overlay" @click.self="close">
    <div class="modal-card">
      <span class="close-btn" @click="close">&times;</span>

      <h2 class="modal-title">{{ isSignup ? "Sign Up" : "Login" }}</h2>

      <form @submit.prevent="submit" class="modal-form">
        <input type="text" v-model="username" placeholder="Username" required />
        <input v-if="isSignup" type="email" v-model="email" placeholder="Email" required />
        <input type="password" v-model="password" placeholder="Password" required />
        <button type="submit">{{ isSignup ? "Sign Up" : "Login" }}</button>
      </form>

      <div class="switch-text">
        <span v-if="isSignup">
          Already have an account? <a href="#" @click.prevent="toggleForm">Login</a>
        </span>
        <span v-else>
          Don't have an account? <a href="#" @click.prevent="toggleForm">Sign Up</a>
        </span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits, watch } from "vue";
import axios from "axios";

const props = defineProps({ modelValue: Boolean });
const emit = defineEmits(["update:modelValue"]);

const dialog = ref(props.modelValue);
watch(() => props.modelValue, val => (dialog.value = val));
watch(dialog, val => emit("update:modelValue", val));

const isSignup = ref(true);

const username = ref("");
const email = ref("");
const password = ref("");

const close = () => {
  dialog.value = false;
  resetForm();
};

const toggleForm = () => {
  isSignup.value = !isSignup.value;
  resetForm();
};

const resetForm = () => {
  username.value = "";
  email.value = "";
  password.value = "";
};

const submit = async () => {
  try {
    if (isSignup.value) {
      // Sign Up API call
      const response = await axios.post("http://127.0.0.1:8000/sign_up", {
        username: username.value,
        email: email.value,
        password: password.value,
      });
      console.log("Sign Up successful, token:", response.data.access_token);
      alert("Sign Up successful!");
    } else {
      // Login API call (OAuth2PasswordRequestForm expects username & password)
      const formData = new URLSearchParams();
      formData.append("username", username.value);
      formData.append("password", password.value);

      const response = await axios.post("http://127.0.0.1:8000/sign_in", formData);
      console.log("Login successful, token:", response.data.access_token);
      alert("Login successful!");
    }
    close();
  } catch (err) {
    console.error("Error:", err.response?.data || err.message);
    alert(err.response?.data?.detail || "Error occurred");
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  z-index: 1000;
}

.modal-card {
  background: #fff;
  border-radius: 10px;
  width: 100%;
  max-width: 380px;
  padding: 20px;
  position: relative;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 15px;
  font-size: 24px;
  font-weight: bold;
  color: #666;
  cursor: pointer;
}

.modal-title {
  margin-bottom: 20px;
  text-align: center;
  font-size: 22px;
  color: #333;
}

.modal-form {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.modal-form input {
  padding: 10px 12px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
  outline: none;
}

.modal-form input:focus {
  border-color: #1976d2;
}

.modal-form button {
  padding: 10px;
  font-size: 16px;
  background-color: #1976d2;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
  transition: background 0.3s;
}

.modal-form button:hover {
  background-color: #135ab5;
}

.switch-text {
  margin-top: 15px;
  text-align: center;
  font-size: 14px;
  color: #555;
}

.switch-text a {
  color: #1976d2;
  text-decoration: none;
  font-weight: 500;
  cursor: pointer;
}

.switch-text a:hover {
  text-decoration: underline;
}

@media (max-width: 400px) {
  .modal-card {
    padding: 15px;
  }

  .modal-form input {
    font-size: 14px;
    padding: 8px 10px;
  }

  .modal-form button {
    font-size: 14px;
    padding: 8px;
  }

  .modal-title {
    font-size: 20px;
  }
}
</style>
