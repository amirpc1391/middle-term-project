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
  isActiveNotification: {
    type: Boolean,
    required: true,
  }

})
</script>

<template>

  <div :class="{'notification-section':true, 'notification-section--active':isActiveNotification}">
    <div :class="`notification-section__content notification-section__content--${type}`">
      <img class="notification-section__img-icon" :src="`src/assets/${type}.png`" :alt="type">
      <div class="notification-section__info">
        <h3 class="notification-section__title">{{ title }}</h3>
        <p class="notification-section__description">
          <slot></slot>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.notification-section {
  max-width: 22rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  gap: 1rem;
  align-items: center;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  margin: 0 auto;
  visibility: hidden;
  opacity: 0;
  transition: all .2s ease-in-out;
  padding: .6rem;
}

.notification-section--active {
  visibility: visible;
  opacity: 1;
}

.notification-section__content {
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

.notification-section__info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.4rem;
}

.notification-section__img-icon {
  width: 3.8rem;
}

.notification-section__title {
  font-size: 1rem;
  font-weight: 700;
  text-transform: capitalize;
}

.notification-section__description {
  font-size: .8rem;
}

.notification-section__content--notice {
  background-color: var(--color_1791ba);
}

.notification-section__content--success {
  background-color: var(--color_darkgreen);
}

.notification-section__content--danger {
  background-color: var(--color_darkred);
}
</style>