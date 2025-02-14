<template>
  <div v-if="logs.length === 0" class="no-logs-container">
    <svg width="120" height="120" viewBox="0 0 24 24" fill="none" class="log-icon">
      <path d="M3 3h18v18H3V3z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      <path d="M7 14h10M7 10h10M7 6h4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
    <h3>No Logs Yet</h3>
    <p>Logs will appear once events are recorded. Check back later or refresh.</p>
    <button @click="refreshLogs" class="refresh-btn">Refresh</button>
  </div>

  <div v-else class="log-list">
    <div v-for="(log, index) in logs" :key="index" class="log-item">
      <span :class="'log-level log-' + log.level.toLowerCase()">{{ log.level }}</span>
      <p class="log-message">{{ log.message }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    logs: {
      type: Array,
      required: true
    }
  },
  methods: {
    refreshLogs() {
      this.$emit("refresh"); // Trigger refresh event for parent component
    }
  }
};
</script>

<style scoped>
/* Empty Logs Styling */
.no-logs-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  text-align: center;
  color: #6b7280; /* Neutral Gray */
}

.log-icon {
  fill: none;
  stroke: #9ca3af; /* Soft Gray */
  stroke-width: 1.5;
  margin-bottom: 1rem;
}

h3 {
  font-size: 1.5rem;
  font-weight: 600;
  color: #374151; /* Dark Gray */
}

p {
  font-size: 1rem;
  color: #6b7280; /* Neutral Gray */
}

/* Refresh Button */
.refresh-btn {
  background: #3b82f6; /* Blue */
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  margin-top: 1rem;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.2s ease-in-out;
}

.refresh-btn:hover {
  background: #2563eb; /* Darker Blue */
}

/* Logs List */
.log-list {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 1rem;
}

.log-item {
  display: flex;
  align-items: center;
  padding: 0.75rem;
  border: 1px solid #e5e7eb;
  border-radius: 5px;
  background: #f9fafb;
}

.log-level {
  font-weight: bold;
  padding: 0.2rem 0.5rem;
  border-radius: 3px;
  text-transform: uppercase;
  margin-right: 0.75rem;
}

.log-message {
  color: #374151;
  font-size: 0.9rem;
}

/* Log Level Colors */
.log-INFO {
  background: #dbeafe;
  color: #1e40af;
}

.log-WARN {
  background: #fef3c7;
  color: #b45309;
}

.log-ERROR {
  background: #fee2e2;
  color: #b91c1c;
}
</style>
