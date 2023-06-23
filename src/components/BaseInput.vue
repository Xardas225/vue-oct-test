<script setup>
import { defineProps, defineEmits, toRefs, computed } from "vue";

const emit = defineEmits(["update:input"]);

const props = defineProps({
  type: { type: String, default: "text" },
  label: { type: String, default: "" },
  placeholder: { type: String, default: "" },
  disabled: { type: Boolean, default: false },
  input: String, 
});

const { input, type, label, placeholder, disabled } = toRefs(props);

const inputComputed = computed({
  get: () => input.value,
  set: (val) => emit("update:input", val),
});
</script>

<template>
  <div>
    <label class="block uppercase tracking-wide text-xs font-bold mb-2">{{
      label
    }}</label>
    <input
      class="apperance-none block w-full text-gray-700 border border-gray-400 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus: border-gray-500"
      :type="type"
      :placeholder="placeholder"
      v-model="inputComputed"
      :disabled="disabled"
      :class="[disabled ? 'bg-gray-200' : 'bg-white']"
    />
  </div>
</template>
