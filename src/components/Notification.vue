<script setup>
defineProps({
  type: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  // description: {
  //   type: String,
  //   required: true,
  // },

})
</script>

<template>
  <div :class="`notification notification--${type}`">
    <img class="notification__img-icon" :src="`src/assets/${type}.png`" :alt="type">
    <div class="notification__info">
      <h3 class="notification__title">{{ title }}</h3>
      <p class="notification__description"><slot></slot></p>
    </div>
  </div>
</template>

<style scoped>
.notification {
  color: var(--color_dee2e6);
  border-radius: 8px;
  padding: 1rem;
  max-width: 22rem;
  line-height: 1.4;
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 0.8rem;
}
.notification__info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.4rem;
}
.notification__img-icon {
 width: 60px;
}

.notification__title {
  font-size: 1rem;
  font-weight: 700;
  text-transform: capitalize;
}

.notification__description {
  font-size: .8rem;
}

.notification--notice {
  background-color: var(--color_1791ba);
}

.notification--success {
  background-color: var(--color_darkgreen);
}

.notification--danger {
  background-color: var(--color_darkred);
}
</style>