<template>
  <div class="calendar">
    <div class="header">
      <button @click="prevMonth">前月</button>
      <h1>{{ currentYear }}年 {{ currentMonth + 1 }}月</h1>
      <button @click="nextMonth">来月</button>
    </div>
    <div class="calendar-grid">
      <div
        class="day-name"
        v-for="(day, index) in dayNames"
        :key="index"
        :class="{
          sunday: index === 0,
          saturday: index === 6
        }"
      >
        {{ day }}
      </div>
      <div
        class="day"
        v-for="(day, index) in blankDays"
        :key="'blank-' + index"
      ></div>
      <div
        class="day"
        v-for="(day, index) in daysInMonth"
        :key="'day-' + index"
        :class="{ today: isToday(day) }"
      >
        {{ day }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 今日の日付情報
const today = new Date()
const todayYear = today.getFullYear()
const todayMonth = today.getMonth()
const todayDate = today.getDate()

// カレンダー表示中の年月
const currentYear = ref(todayYear)
const currentMonth = ref(todayMonth)

const dayNames = ['日', '月', '火', '水', '木', '金', '土']

// 今月の日数
const daysInMonth = computed(() => {
  const lastDay = new Date(currentYear.value, currentMonth.value + 1, 0).getDate()
  return Array.from({ length: lastDay }, (_, i) => i + 1)
})

// 空白（日曜始まり）
const blankDays = computed(() => {
  const firstDay = new Date(currentYear.value, currentMonth.value, 1).getDay()
  return Array.from({ length: firstDay })
})

// 月送り
function prevMonth() {
  if (currentMonth.value === 0) {
    currentMonth.value = 11
    currentYear.value--
  } else {
    currentMonth.value--
  }
}

function nextMonth() {
  if (currentMonth.value === 11) {
    currentMonth.value = 0
    currentYear.value++
  } else {
    currentMonth.value++
  }
}

// 今日かどうか判定
function isToday(day) {
  return (
    day === todayDate &&
    currentMonth.value === todayMonth &&
    currentYear.value === todayYear
  )
}
</script>

<style scoped>
.calendar {
  max-width: 400px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
}
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  color: #42b983;
  margin: 0;
}
button {
  background-color: #42b983;
  border: none;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
}
.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 5px;
  margin-top: 20px;
}
.day-name {
  font-weight: bold;
  text-align: center;
}
/* 日曜を赤に、土曜を青に */
.sunday {
  color: red;
}
.saturday {
  color: blue;
}
.day {
  height: 40px;
  text-align: center;
  line-height: 40px;
  border: 1px solid #eee;
  border-radius: 4px;
  background-color: #f9f9f9;
}
/* 今日の日付に薄い黄色背景 */
.today {
  background-color: #fffacd;
  font-weight: bold;
}
</style>
