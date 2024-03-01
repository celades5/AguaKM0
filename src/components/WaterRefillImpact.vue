<template>
  <div>
    <h1>Water Refill Impact Calculator</h1>
    <div>
      <label for="refills">Number of Water Refills:</label>
      <!--button ensures that min of refills > 0 -->
      <input type="number" id="refills" v-model="refills" min="0">
    </div>
    <button @click="calculateImpact">Calculate Impact</button>
    <div class="result" v-if="impactCalculated">{{ impactMessage() }}</div>
  </div>
</template>
  
<script setup lang="ts">
import { ref } from 'vue';
import VueClipboard from 'vue-clipboard3';
// import library for CountUp animation

// Define reactive variables to store the data
// Each variable is associated with a specific piece of data that the application needs to track
const refills = ref(0); // stores the number of water refills entered by the user
const impactCalculated = ref(false); // boolean flag that indicates whether the environmental impact has been calculated
const bottlesSaved = ref(0);
const plasticSaved = ref(0);
const co2Saved = ref(0);
// using the ref function, you ensure that these variables are reactive

const calculateImpact = () => {
  bottlesSaved.value = refills.value * 2;
  plasticSaved.value = bottlesSaved.value * 0.012; 
  co2Saved.value = bottlesSaved.value * 0.08;
  impactCalculated.value = true;
};

const impactMessage = () => {
  return `You saved ${bottlesSaved.value} plastic bottles (${plasticSaved.value} kg) and ${co2Saved.value} kg of CO2 by refilling water ${refills.value} times.`;
};


// CSS for the script
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
