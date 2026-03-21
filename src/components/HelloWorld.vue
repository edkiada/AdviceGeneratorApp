<script setup>
  import { ref, onMounted} from 'vue'

  const adviceData = ref({
    id: '0',
    advice: "loading...",
  });
  const isLoading = ref(true);

  const fetchAdvice = async () => {
    try {
      const URL = `https://api.adviceslip.com/advice?t=${new Date().getTime()}`;
      const response = await fetch(URL);
      const data = await response.json();

      adviceData.value = {
        id: data.slip.id,
        advice: data.slip.advice,
      }
    }
    catch (error) {
      console.error("Error fetching advice:", error);
    }
    finally {
      isLoading.value = false;
    }
  };

  onMounted(() => {
    fetchAdvice();
  });
</script>

<template>
  <main class="container">
    <p class="adviceId">ADVICE #{{ adviceData.id }}</p>
    <p class="adviceText">“{{ adviceData.advice }}”</p>
    <img src="../assets/pattern-divider-desktop.svg" alt="divider" class="divider" />
    <button @click="fetchAdvice" class="dice-button">
      <img src="../assets/icon-dice.svg" alt="dice" class="dice"/>
  </button>
  </main>
</template>
