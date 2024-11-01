<script setup>
import { ref } from "vue";

const dates = ref();
const ttldays = ref(null);

const handlePlusDays = (ttlday) => {
  ttldays.value = ttlday;
  console.log(ttldays.value);
  if (!dates.value || dates.value[0] === null || dates.value[1] === null) {
    return;
  }
  const start = dates.value[0];
  const end = dates.value[1];
  switch (ttlday) {
    case 0:
      dates.value = []
      break;
    case 1:
      dates.value = [start, new Date(end.setDate(end.getDate() + 1))];
      break;
    case 3:
      dates.value = [start, new Date(end.setDate(end.getDate() + 3))];
      break;
    case 5:
      dates.value = [start, new Date(end.setDate(end.getDate() + 5))];
      break;
    case 7:
      dates.value = [start, new Date(end.setDate(end.getDate() + 7))];
      break;
    case 15:
      dates.value = [start, new Date(end.setDate(end.getDate() + 15))];
      break;
    default:
      break;
  }
};

const shouldDisableDate = () => {
  if (!dates.value || dates.value[0] === null || dates.value[1] === null) {
    return true;
  }
  return false;
};

const parseFormatDate = (date) => {
  if (!date) {
    return "";
  }
  return new Date(date).toLocaleDateString("es-MX", {
    year: "numeric",
    month: "2-digit",
    day: "2-digit",
  });
}; 
</script>
<template>
  <main>  
    <h4 class="text-green-700 font-bold text-sm mx-auto text-center">Calendar </h4>
    <div class="bg-gray-100 rounded-sm shadow-sm max-w-md min-h-[600px] mx-auto flex justify-center p-5 ">
      <div class="flex flex-col gap-y-3">
        <div class="flex mb-2 justify-center">
          <button 
            @click="handlePlusDays(0)"
            :disabled="shouldDisableDate()"
            :class="[
              ttldays == 0 ? 'bg-green-700 text-white' : 'bg-white text-black',
              shouldDisableDate() ? 'cursor-not-allowed text-gray-300' : ''
            ]"
            class=" flex justify-center items-center border border-gray-200 px-2 py-1 min-w-9 rounded-l">0</button>
          <button 
            @click="handlePlusDays(1)"
            :class="[
              ttldays == 1 ? 'bg-green-700 text-white' : 'bg-white text-black',
              shouldDisableDate() ? 'cursor-not-allowed text-gray-300' : ''
            ]"
            class=" flex justify-center items-center border border-gray-200 px-2 py-1 min-w-9">1</button>
          <button 
            @click="handlePlusDays(3)"
            :class="[
              ttldays == 3 ? 'bg-green-700 text-white' : 'bg-white text-black',
              shouldDisableDate() ? 'cursor-not-allowed text-gray-300' : ''
            ]"
            class=" flex justify-center items-center border border-gray-200 px-2 py-1 min-w-9">3</button>
          <button 
            @click="handlePlusDays(5)"
            :class="[
              ttldays == 5 ? 'bg-green-700 text-white' : 'bg-white text-black',
              shouldDisableDate() ? 'cursor-not-allowed text-gray-300' : ''
            ]"
            class=" flex justify-center items-center border border-gray-200 px-2 py-1 min-w-9">5</button>
          <button 
            @click="handlePlusDays(7)"
            :class="[
              ttldays == 7 ? 'bg-green-700 text-white' : 'bg-white text-black',
              shouldDisableDate() ? 'cursor-not-allowed text-gray-300' : ''
            ]"
            class=" flex justify-center items-center border border-gray-200 px-2 py-1 min-w-9">7</button>
          <button 
            @click="handlePlusDays(15)"
            :class="[
              ttldays == 15 ? 'bg-green-700 text-white' : 'bg-white text-black',
              shouldDisableDate() ? 'cursor-not-allowed text-gray-300' : ''
            ]"
            class=" flex justify-center items-center border border-gray-200 px-2 py-1 min-w-9 rounded-r">15</button>
        </div>
        <DatePicker 
          v-model="dates" 
          selectionMode="range" 
          inline 
          showWeek 
          :manualInput="false" 
          class="block"/>

        <span class="bg-gray-300 h-8 w-full rounded-md flex justify-center items-center text-green-950 text-sm" v-if="dates">
          {{ parseFormatDate(dates[0]) }} - {{ parseFormatDate(dates[1]) }}
        </span>
      </div>
    </div>
  </main>
</template>