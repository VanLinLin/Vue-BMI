<template>
  <div class="py-2 m-auto">
    <label for="price" class="block text-sm font-medium text-white"
      >{{ label_text }}
    </label>
    <div class="mt-1 rounded-md m-auto">
      <input
        class="
          focus:ring-indigo-500 focus:border-indigo-500
          block
          sm:text-sm
          border-2 border-gray-700
          rounded-md
          m-auto
        "
        placeholder="請輸入身高"
        :value="props.modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
      <div
        class="
          absolute
          inset-y-0
          right-4
          pl-3
          flex
          items-center
          pointer-events-none
        "
      >
        <span class="text-gray-500 sm:text-sm">{{ unit_text }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  modelValue: { type: Number },
  label_text: { type: String },
  unit_text: { type: String },
});
</script>