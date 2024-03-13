<script setup>
import { ref } from 'vue';

// State
const currentJersey = ref('--');
const currentJerseyImage = ref('--');
const jerseyList = [
  { name: '--', value: '' },
  { name: 'Anaheim', value: 'Anaheim' },
  { name: 'Buffalo', value: 'Buffalo' }
];

// Actions
async function fetchCurrentJerseyImage(jersey) {
  console.log(jersey);
  const response = await fetch('https://media.d3.nhle.com/image/private/t_q-best/prd/assets/nhl/logos/nhl_shield_wm_on_dark_fqkbph');
  const jerseyImage = await response.text();
  // document.body.insertAdjacentHTML("beforeend", jerseyImage);
  document.getElementById('current-jersey-image').insertAdjacentHTML('beforeend', jerseyImage);
  console.log({ jerseyImage });
}
</script>

<!-- View -->
<template>
  <nav>NHL | AHL</nav>
  <p>Dropdown for team to view in selected league (Buffalo, Seattle, etc.)</p>
  <label for="jersey-select">Choose a jersey:</label>
  <select
    name="jerseys"
    id="jersey-select"
    v-model="currentJersey"
    @change="(event) => fetchCurrentJerseyImage(event.target.value)"
  >
    <option v-for="(jerseyItem, index) in jerseyList" :value="jerseyItem.value" :key="index">
      {{ jerseyItem.name }}
    </option>
  </select>
  <br />
  <span>{{ currentJersey }}</span>
  <br />
  <svg id="current-jersey-image">{{ currentJerseyImage }}</svg>
  <br />
  <span>Star rating: ⭐️⭐️⭐️⭐️⭐️</span>
</template>
