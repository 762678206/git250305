<!-- src/components/Checkout.vue -->
<template>
  <div class="checkout">
    <h2>已选座位：</h2>
    <ul>
      <li v-for="seatId in selectedSeats" :key="seatId">{{ seatId }}</li>
    </ul>
    <p>总价：{{ totalPrice }} 元</p>
    <button @click="checkout">结算</button>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  selectedSeats: Array,
  seats: Array // 座位布局二维数组
});

const totalPrice = computed(() => {
  let sum = 0;
  props.selectedSeats.forEach(seatId => {
    for (const row of props.seats) {
      const seat = row.find(s => s.id === seatId);
      if (seat) {
        sum += seat.price;
        break;
      }
    }
  });
  return sum;
});

const checkout = () => {
  if (props.selectedSeats.length === 0) {
    alert('请先选择座位！');
    return;
  }
  alert('结算成功！');
  // 实际应用中，这里应发送请求到后端
};
</script>

<style scoped>
.checkout {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
ul {
  list-style-type: none;
  padding: 0;
}
button {
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}
</style>
