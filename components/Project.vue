<script setup>
defineProps({
  title: String,
  index: Number,
  modal: Object,
});

defineEmits(["onMouseEnter", "onMouseLeave"]);
</script>

<template>
  <div
    @mouseenter="$emit('onMouseEnter', index)"
    @mouseleave="$emit('onMouseLeave', index)"
    class="group flex w-full justify-between items-center px-[100px] py-[50px] border-t-[1px] ease-linear border-[rgb(201, 201, 201)] cursor-pointer transition-all duration-[0.2s] last-of-type:border-b-[1px] hover:opacity-50"
  >
    <h2
      class="group-hover:translate-x-[-10px] text-6xl font-normal duration-[0.4s] ease-linear transition-all"
    >
      {{ title }}
    </h2>
    <p
      class="duration-[0.4s] ease-linear transition-all font-light group-hover:translate-x-[10px]"
    >
      Design & Development
    </p>
  </div>
</template>
