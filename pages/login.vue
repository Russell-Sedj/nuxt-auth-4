<template>
  <div>
    <h1>Sign In</h1>
    <div v-if="errorMsg" class="error">{{ errorMsg }}</div>
    <form @submit.prevent="signIn">
      <input type="email" v-model="email" placeholder="Email" />
      <input type="password" v-model="password" placeholder="Password" />
      <button type="submit">Sign In</button>
    </form>
  </div>
</template>

<script setup>
const router = useRouter();

const client = useSupabaseClient();
const email = ref("");
const password = ref("");
const errorMsg = ref("");

async function signIn() {
  try {
    const { error } = await client.auth.signInWithPassword({
      email: email.value,
      password: password.value,
    });
    if (error) throw error;
    router.push("/profile");
  } catch (error) {
    errorMsg.value = error.message;
  }
}
</script>

<style scoped></style>
