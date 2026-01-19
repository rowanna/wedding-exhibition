<template>
  <div class="countdown-container">
    <h1 class="title">WEDDING EXHIBITION</h1>
    
    <div v-if="!isActive" class="countdown">
      <p class="countdown-text">전시회 오픈까지 남은 시간</p>
      <p class="countdown-text-small">2월 10일부터 1달간 전시 됩니다.</p>
      <div class="time-container">
        <div class="time-block">
          <span class="time-value">{{ days }}</span>
          <span class="time-label">Days</span>
        </div>
        <div class="time-block">
          <span class="time-value">{{ hours }}</span>
          <span class="time-label">hours</span>
        </div>
        <div class="time-block">
          <span class="time-value">{{ minutes }}</span>
          <span class="time-label">minutes</span>
        </div>
        <div class="time-block">
          <span class="time-value">{{ seconds }}</span>
          <span class="time-label">seconds</span>
        </div>
      </div>
    </div>
    
    <button 
      class="exhibition-button"
      @click="goToExhibition"
    >
      GO TO EXHIBITION
    </button>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue';


// const targetDate = new Date();
// targetDate.setDate(targetDate.getDate() + ((1 + 7 - targetDate.getDay()) % 7 || 7)); // Next Monday

const targetDate = new Date(2026, 1, 10); 
targetDate.setHours(0, 0, 0, 0); // Set to midnight

const now = ref(new Date());
const isActive = computed(() => now.value >= targetDate);

const timeLeft = computed(() => {
  return Math.max(0, targetDate.getTime() - now.value.getTime());
});

const days = computed(() => {
  return Math.floor(timeLeft.value / (1000 * 60 * 60 * 24));
});

const hours = computed(() => {
  return Math.floor((timeLeft.value % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
});

const minutes = computed(() => {
  return Math.floor((timeLeft.value % (1000 * 60 * 60)) / (1000 * 60));
});

const seconds = computed(() => {
  return Math.floor((timeLeft.value % (1000 * 60)) / 1000);
});

let timer: number;

onMounted(() => {
  timer = window.setInterval(() => {
    now.value = new Date();
  }, 1000);
});

onUnmounted(() => {
  if (timer) clearInterval(timer);
});

const goToExhibition = () => {
  if(!isActive.value) {
    alert('전시회가 아직 시작되지 않았습니다.');
    return;
  }
  // TODO: Add your exhibition URL here
  alert('전시회 페이지로 이동합니다.');
  // window.location.href = 'YOUR_EXHIBITION_URL';
};
</script>

<style scoped>
.countdown-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 20px;
  background-color: #f8f8f8;
  font-family: 'Noto Sans KR', sans-serif;
  text-align: center;
  /* margin: 30px; */
}

.title {
  font-size: 2.2rem;
  color: #DC340C;
  margin-bottom: 2rem;
  font-family: 'Instrument Serif', serif;
  font-weight: 400;
  letter-spacing: 1px;
}

.countdown {
  width: 80%;
  max-width: 400px;
  background: white;
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.countdown-text {
  font-size: 1.2rem;
  color: #666;
  margin-bottom: 1.5rem;
}
.countdown-text-small {
  font-size: 1.0rem;
  margin-bottom: 1.5rem
}

.time-container {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
}

.time-block {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
}

.time-value {
  font-size: 2.2rem;
  font-family: 'Instrument Serif', serif;
  color: #333;
  background: #f8f8f8;
  border-radius: 8px;
  padding: 0.2rem;
  width: 100%;
  margin-bottom: 0.5rem;
  font-weight: 400;
}

.time-label {
  font-size: 0.9rem;
  color: #666;
}

.exhibition-button {
  background-color: #DC340C;
  color: white;
  border: none;
  border-radius: 50px;
  padding: 1rem 2rem;
    font-family: 'Instrument Serif', serif;

  font-size: 1.2rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(220, 52, 12, 0.3);
  width: 100%;
  max-width: 300px;
  margin-top: 2rem;
  letter-spacing: 1.5px;
}

.exhibition-button:hover {
  background-color: #b82a0a;
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(220, 52, 12, 0.4);
}

.exhibition-button:active {
  transform: translateY(0);
}

/* Responsive Design */
@media (max-width: 480px) {
  .title {
    font-size: 1.8rem;
  }
  
  .time-value {
    font-size: 1.8rem;
  }
  
  .time-label {
    font-size: 0.8rem;
  }
  
  .exhibition-button {
    font-size: 1.1rem;
    padding: 0.9rem 1.8rem;
  }
}
</style>