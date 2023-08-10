<template>
  <div>
    <h1>Sign Up</h1>
    <div v-if="errorMsg" class="error">{{ errorMsg }}</div>
    <div v-if="successMsg" class="success">{{ successMsg }}</div>
    <form @submit.prevent="signUp">
      <input type="email" v-model="email" placeholder="Email" />
      <input type="password" v-model="password" placeholder="Password" />
      <button type="submit">Sign Up</button>
    </form>
  </div>
  <form @submit.prevent="signIn"></form>
</template>

<script setup>
const client = useSupabaseClient();
const email = ref("");
const password = ref("");
const errorMsg = ref("");
const successMsg = ref("");

async function signUp() {
  try {
    const { user, error } = await client.auth.signUp({
      email: email.value,
      password: password.value,
    });
    if (error) throw error;
    successMsg.value = "Check your email for confirmation link";
  } catch (error) {
    errorMsg.value = error.message;
  }
}
</script>

<style scoped></style>
