<!-- src/App.vue -->
<template>
  <div class="movie-ticket-app">
    <h1>电影选座系统</h1>
    <SeatLayout :seats="seats" :selectedSeats="selectedSeats" @select="selectSeat" @unselect="unselectSeat" />
    <Checkout :selectedSeats="selectedSeats" :seats="seats" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SeatLayout from './components/SeatLayout.vue';
import Checkout from './components/Checkout.vue';

// 示例座位数据（实际应从后端获取）
const seats = ref([
  [
    { id: '1-1', status: 'available', price: 10 },
    { id: '1-2', status: 'booked', price: 10 },
    { id: '1-3', status: 'available', price: 10 }
  ],
  [
    { id: '2-1', status: 'available', price: 10 },
    { id: '2-2', status: 'available', price: 10 },
    { id: '2-3', status: 'booked', price: 10 }
  ]
]);

const selectedSeats = ref([]);

const selectSeat = (seatId) => {
  selectedSeats.value.push(seatId);
};

const unselectSeat = (seatId) => {
  const index = selectedSeats.value.indexOf(seatId);
  if (index > -1) {
    selectedSeats.value.splice(index, 1);
  }
};
</script>

<style>
.movie-ticket-app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}
</style>
