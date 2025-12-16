<template>
  <div class="custom-select" @click="toggleSelect">
    <div class="selected-option">
      {{ selectedText }}
      <span :class="['arrow', { open: isOpen }]"></span>
    </div>

    <ul v-if="isOpen" class="options">
      <li
        v-for="(op, index) in options"
        :key="index"
        class="option"
        @click.stop="selectOption(op)"
      >
        {{ op }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  modelValue: String,
  options: Array,
});

const emit = defineEmits(["update:modelValue"]);

const isOpen = ref(false);
const selectedText = ref(props.modelValue || "Selecione");

const toggleSelect = () => {
  isOpen.value = !isOpen.value;
};

const selectOption = (texto) => {
  selectedText.value = texto;
  emit("update:modelValue", texto);
  isOpen.value = false;
};
</script>

<style scoped>
.custom-select {
  width: 100%;
  position: relative;
  cursor: pointer;
  font-family: inherit;
}

.selected-option {
  background: white;
  border: 2px solid #ddd;
  padding: 12px 16px;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.arrow {
  width: 10px;
  height: 10px;
  border-right: 2px solid #555;
  border-bottom: 2px solid #555;
  transform: rotate(45deg);
  transition: 0.3s;
}

.arrow.open {
  transform: rotate(-135deg);
}

.options {
  position: absolute;
  top: 55px;
  left: 0;
  right: 0;
  background: white;
  border: 2px solid #ddd;
  border-radius: 8px;
  box-shadow: 0px 4px 10px rgba(0,0,0,0.1);
  z-index: 10;
}

.option {
  padding: 12px 16px;
  border-bottom: 1px solid #eee;
}

.option:hover {
  background: #f3f3f3;
}
</style>
