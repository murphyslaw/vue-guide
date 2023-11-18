<script setup>
import { computed, ref } from "vue";

const binary = ref("");
const decimal = computed(() => {
  if (!binary.value) return null;

  return parseInt(binary.value, 2);
});

function onInput(event) {
  const element = event.target;
  const valid = element.reportValidity();

  if (valid) {
    element.removeAttribute("invalid");
  } else {
    element.setAttribute("invalid", true);
  }

  console.log(event);

  return;
}
</script>

<template>
  <div class="converter">
    <section>
      <label class="headline" for="binaryConverter">Binary</label>

      <input
        v-model="binary"
        id="binaryConverter"
        type="text"
        inputmode="numeric"
        pattern="[0-1]{0,8}"
        maxlength="8"
        @input="onInput"
      />
    </section>

    <section>
      <span class="headline">Decimal</span>

      <span class="decimal">{{ decimal }}</span>
    </section>
  </div>
</template>

<style scoped>
section {
  height: 50vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
}

input,
.decimal {
  display: block;
  font-size: 5rem;
  text-align: center;
}

input {
  background-color: #70a9a1;
  color: #1f3330;
  opacity: 0.8;
  border: none;
  border-bottom: 1px solid #1f3330;
  transition: 100ms all;
}

input[invalid] {
  border-color: #b00020;
}

input:hover {
  opacity: 1;
  border-color: #1f3330;
}

input:focus {
  opacity: 1;
  outline: none;
  border-width: 0.2rem;
}

input:focus[invalid] {
  border-color: #b00020;
}

.headline {
  display: block;
  font-weight: bold;
  font-size: 10rem;
  text-transform: uppercase;
}

.converter {
  background: #cfd7c7;
  font-family: sans-serif;
  color: #1f3330;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-around;
  text-align: center;
}
</style>
