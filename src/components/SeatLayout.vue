<!-- src/components/SeatLayout.vue -->
<template>
  <div class="seat-layout">
    <div v-for="(row, rowIndex) in seats" :key="rowIndex" class="row">
      <SeatSelector
        v-for="(seat, colIndex) in row"
        :key="colIndex"
        :seat="seat"
        :selectedSeats="selectedSeats"
        @select="selectSeat"
        @unselect="unselectSeat"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SeatSelector from './SeatSelector.vue';

const props = defineProps({
  seats: Array,
  selectedSeats: Array
});

const emit = defineEmits(['select', 'unselect']);

const selectSeat = (seatId) => {
  emit('select', seatId);
};

const unselectSeat = (seatId) => {
  emit('unselect', seatId);
};
</script>

<style scoped>
.seat-layout {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.row {
  display: flex;
}
</style>
