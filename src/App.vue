<script setup>
import { ref } from "vue";

const display = ref("");

const buttons = [
  { value: "AC", type: "clear" },
  { value: "DEL", type: "delete" },
  { value: ".", type: "operator" },
  { value: "/", type: "operator" },

  { value: "7" },
  { value: "8" },
  { value: "9" },
  { value: "*", type: "operator" },

  { value: "4" },
  { value: "5" },
  { value: "6" },
  { value: "-", type: "operator" },

  { value: "1" },
  { value: "2" },
  { value: "3" },
  { value: "+", type: "operator" },

  { value: "000" },
  { value: "00" },
  { value: "0" },
  { value: "=", type: "operator" },
];

const update = (value) => {
  if (value === "AC") return (display.value = "");
  if (value === "DEL") return (display.value = display.value.slice(0, -1));
  if (value === "=") return (display.value = eval(display.value));

  display.value += value;
};
</script>

<template>
  <div class="calculator">
    <input type="text" v-model="display" class="display" disabled />

    <div class="buttons">
      <button
        v-for="btn in buttons"
        :key="btn.value"
        @click="update(btn.value)"
        :class="`button button_${btn.type || 'default'}`"
      >
        {{ btn.value }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.calculator {
  width: 300px;
  background: #222;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.display {
  width: 100%;
  height: 60px;
  font-size: 2rem;
  text-align: right;
  padding: 10px;
  margin-bottom: 20px;
  background: #333;
  color: #fff;
  border: none;
  border-radius: 5px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.button {
  width: 60px;
  height: 60px;
  font-size: 1.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background: #444;
  color: white;
  transition: background 0.2s;

  &:hover {
    background: #555;
  }
}

.button_clear {
  background: #d9534f;
  &:hover {
    background: #c9302c;
  }
}

.button_delete {
  background: #f0ad4e;
  &:hover {
    background: #ec971f;
  }
}

.button_operator {
  background: #0275d8;
  &:hover {
    background: #025aa5;
  }
}
</style>
