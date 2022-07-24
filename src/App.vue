<template>
  <div class="w-80 m-auto text-center shadow-lg rounded-md bg-black">
    <div class="mt-9 text-[color:#34D399]">
      <div class="pt-8 text-6xl">BMI計算器</div>
    </div>

    <div class="mt-6 text-center">
      <InputGroup v-model="height" label_text="身高" class="mx-6" />
      <div class="m-auto text-white">
        {{ isNaN(height) ? 0 : height / 100 }}
        公尺
      </div>
    </div>

    <div class="mt-6 text-center">
      <InputGroup v-model="weight" label_text="體重" class="mx-6" />
      <div class="mx-6 text-white">{{ weight }}公斤</div>
    </div>

    <div class="mt-8 flex justify-center">
      <div class="text-5xl text-[#9FA6B2]">BMI:</div>
      <div class="text-3xl mt-3" :class="result.info[2]">
        {{ result.BMI }}
      </div>
    </div>

    <div class="mt-8 flex justify-center">
      <div class="text-md w-60 pt-4 pb-4 rounded-lg bg-[#FDE68A]">
        你的體重是「{{ result.info[0] }}」
      </div>
    </div>

    <div class="mt-8">
      <table class="m-auto w-56">
        <tr
          v-for="info in info_map"
          :key="info.index"
          class="mt-2"
          :class="info[2]"
        >
          <td class="text-left">{{ info[0] }}</td>
          <td class="text-right">{{ info[1] }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import InputGroup from "./components/InputGroup.vue";

let info_map = [
  ["過輕", "BMI<18.5", "text-[color:#DBFF00]"],
  ["正常範圍", "18.5≦BMI<24", "text-[color:#50DF84]"],
  ["過重", "24≦BMI<27", "text-[color:#FBBF24]"],
  ["輕度肥胖", "27≦BMI<30", "text-[color:#FF6B00]"],
  ["中度肥胖", "30≦BMI<35", "text-[color:#FF4D00]"],
  ["重度肥胖", "≧35", "text-[color:#EF4545]"],
  ["", "", "text-[color:#FF0000]"],
];

const height = ref("");
const weight = ref("");
const result = computed(() => {
  let bmi = (weight.value / Math.pow(height.value / 100, 2)).toFixed(2);

  if (isNaN(bmi)) {
    return { BMI: "請輸入數字", info: info_map[6] };
  } else if (parseFloat(height.value) === 0 || parseFloat(weight.value) === 0) {
    return { BMI: "請輸入數字", info: info_map[6] };
  } else {
    if (bmi < 18.5) {
      return { BMI: bmi, info: info_map[0] };
    } else if (18.5 <= bmi && bmi < 24) {
      return { BMI: bmi, info: info_map[1] };
    } else if (24 <= bmi && bmi < 27) {
      return { BMI: bmi, info: info_map[2] };
    } else if (27 <= bmi && bmi < 30) {
      return { BMI: bmi, info: info_map[3] };
    } else if (30 <= bmi && bmi < 35) {
      return { BMI: bmi, info: info_map[4] };
    } else {
      return { BMI: bmi, info: info_map[5] };
    }
  }
});
</script>

<style>
html {
  background-color: rgb(55, 181, 185);
}
</style>
