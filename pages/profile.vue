<template>
  <div>
    <h1>Email: {{ user.email }}</h1>
    <button @click="logout">Log Out</button>
  </div>
</template>

<script setup>
definePageMeta({
  middleware: ["auth"],
});

const router = useRouter();
const user = useSupabaseUser();
const client = useSupabaseClient();

console.log(user);

async function logout() {
  try {
    const { error } = await client.auth.signOut();
    if (error) {
      console.log("Agaigiagaigaggiagiaigi \n", error);
      throw error;
    }
    router.push("/login");
  } catch (error) {
    console.log("Here is the errorrrrr \n", error);
  }
}
</script>

<style scoped></style>
