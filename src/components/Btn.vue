<script setup>

defineProps({
  type: {
    type: String,
    default: 'default',
  },
  label: {
    type: String,
    required: true,
  },
  imgIcon: {
    type: String,
    default: '',
  },
});
</script>

<template>
  <button :class="['btn', `btn--${type}`]">
    <img v-if="imgIcon" :src="imgIcon" :alt="label" class="btn__img"/>
    {{ label }}
  </button>
</template>

<style scoped>


.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.25rem 0.5rem;
  font-size: 0.8rem;
  line-height: 1.5;
  border-radius: 0.3rem;
  font-weight: 400;
  color: #f8f9fa;
  cursor: pointer;
  box-shadow: none;
  border: none;
  transition: all 0.15s ease-in-out;
  gap: .3rem;
}

.btn__img {
  width: .8rem;
  height: .8rem;
}

.btn--default, .btn--edit {
  background-color: #4dc3ff;
}

.btn--default:hover, .btn--edit:hover {
  background-color: #1791ba;
}

.btn--delete {
  background-color: #e84a67;
}

.btn--delete:hover {
  background-color: #ed2939;
}

.btn--add {
  background-color: #1fa620;
}

.btn--add:hover {
  background-color: #178817;
}

.btn--close {
  background-color: transparent;
  color: #adb5bd;
}

.btn--close:hover {
  background-color: transparent;
  color: #8f979e;
}
</style>
