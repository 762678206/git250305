<!-- src/components/SeatSelector.vue -->
<template>
  <div :class="['seat', { selected: isSelected, booked: seat.status === 'booked' }]" @click="toggleSelect"></div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  seat: Object, // 座位数据
  selectedSeats: Array // 已选座位列表
});

const emit = defineEmits(['select', 'unselect']);

const isSelected = computed(() => props.selectedSeats.includes(props.seat.id));

const toggleSelect = () => {
  if (props.seat.status === 'booked') return; // 已预订座位不可点击
  if (isSelected.value) {
    emit('unselect', props.seat.id);
  } else {
    emit('select', props.seat.id);
  }
};
</script>

<style scoped>
.seat {
  width: 30px;
  height: 30px;
  margin: 5px;
  background-color: #ccc;
  cursor: pointer;
  border-radius: 4px;
}
.seat.selected {
  background-color: #4caf50;
}
.seat.booked {
  background-color: #f44336;
  cursor: not-allowed;
}
</style>
