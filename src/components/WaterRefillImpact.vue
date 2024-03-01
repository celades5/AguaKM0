<template>
  <div>
    <h1>Water Refill Impact Calculator</h1>
    <div>
      <label for="refills">Number of Water Refills:</label>
      <input type="number" id="refills" v-model="refills" min="0">
    </div>
    <button @click="calculateImpact">Calculate Impact</button>
    <div class="result" v-if="impactCalculated">{{ impactMessage() }}</div>
  </div>
</template>
  
<script setup lang="ts">
import { ref } from 'vue';
import VueClipboard from 'vue-clipboard3';

const refills = ref(0);
const impactCalculated = ref(false);
const bottlesSaved = ref(0);
const plasticSaved = ref(0);
const co2Saved = ref(0);

const calculateImpact = () => {
  bottlesSaved.value = refills.value * 0.5; // Assuming 1 refill = 0.5 bottles
  plasticSaved.value = bottlesSaved.value * 0.5; // Assuming 1 bottle = 0.5 kg of plastic
  co2Saved.value = bottlesSaved.value * 0.2; // Assuming 1 bottle = 0.2 kg of CO2
  impactCalculated.value = true;
};

const impactMessage = () => {
  return `You saved ${bottlesSaved.value} plastic bottles (${plasticSaved.value} kg) and ${co2Saved.value} kg of CO2 by refilling water ${refills.value} times.`;
};

</script>
  
<style scoped>

.title {
  font-family: 'Arial', sans-serif;
  font-size: 24px;
  font-weight: bold;
  color: #333; 
  text-align: center;
  margin-bottom: 20px;
}

.result {
  font-size: 24px;
  font-weight: bold;
  color: green;
  transition: color 1s;
}

input[type="number"] {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

button {
  padding: 10px 20px;
  background-color: #4CAF50;
  border: none;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}
button:hover {
  background-color: #45a049;
}
</style>
