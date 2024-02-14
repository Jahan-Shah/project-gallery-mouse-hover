<script setup>
const props = defineProps({
  modal: Object,
  projects: Array,
});

const top = computed(() => {
  return {
    top: props.modal.index * -100 + "%",
  };
});

const cursorLabel = ref(null);
const modalContainer = ref(null);
const active = computed(() => props.modal.active);

const animateElement = (element, properties) => gsap.to(element, properties);

watch(active, (value) => {
  const properties = {
    x: "-50%",
    y: "-50%",
    duration: 0.5,
  };

  CustomEase.create(
    "customEase",
    value ? "0.76, 0, 0.24, 1" : "0.32, 0, 0.67, 0"
  );
  animateElement([modalContainer.value, cursorLabel.value], {
    ...properties,
    scale: value ? 1 : 0,
    ease: "customEase",
  });
});

const onMouseMove = ref(() => {});
onMounted(() => {
  const modal = modalContainer.value;
  const cursor = cursorLabel.value;

  gsap.set([modal, cursor], {
    scale: 0,
    x: "-50%",
    y: "-50%",
  });

  const ease = "power3";
  const containerOptions = { duration: 0.8, ease };
  const cursorLabelOptions = { duration: 0.45, ease };

  let xMoveContainer = gsap.quickTo(modal, "left", containerOptions);
  let yMoveContainer = gsap.quickTo(modal, "top", containerOptions);
  let xMoveCursorLabel = gsap.quickTo(cursor, "left", cursorLabelOptions);
  let yMoveCursorLabel = gsap.quickTo(cursor, "top", cursorLabelOptions);

  onMouseMove.value = (e) => {
    if (modal === null || cursor === null) return;
    const { pageX, pageY } = e;
    xMoveContainer(pageX);
    yMoveContainer(pageY);
    xMoveCursorLabel(pageX);
    yMoveCursorLabel(pageY);
  };

  window.addEventListener("mousemove", onMouseMove.value);
});

onUnmounted(() => {
  window.removeEventListener("mousemove", onMouseMove.value);
});
</script>
<template>
  <div
    ref="modalContainer"
    class="h-[350px] w-[400px] absolute bg-white overflow-hidden pointer-events-none flex items-center justify-center"
  >
    <div
      :style="top"
      class="h-full w-full absolute transition-[top] duration-[0.5s] ease=[cubic-bezier(0.76,0,0.24,1)]"
    >
      <div
        v-for="(project, index) in projects"
        :key="`modal_${index}`"
        :style="{ backgroundColor: project.color }"
        class="h-full w-full flex items-center justify-center"
      >
        <NuxtImg
          class="h-auto w-auto"
          alt="image"
          width="300"
          :src="`/images/${project.src}`"
        />
      </div>
    </div>
  </div>
  <div
    ref="cursorLabel"
    class="w-[80px] h-[80px] rounded-full bg-[#455CE9] text-white absolute z-[2] flex items-center justify-center text-sm font-light pointer-events-none"
  >
    View
  </div>
</template>
