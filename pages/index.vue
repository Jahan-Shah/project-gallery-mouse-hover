<script setup>
const projects = [
  {
    title: "C2 Montreal",
    src: "c2montreal.png",
    color: "#000000",
  },
  {
    title: "Office Studio",
    src: "officestudio.png",
    color: "#8C8C8C",
  },
  {
    title: "Locomotive",
    src: "locomotive.png",
    color: "#EFE8D3",
  },
  {
    title: "Silencio",
    src: "silencio.png",
    color: "#706D63",
  },
];

const modal = shallowRef({
  active: false,
  index: 0,
});

function mouseEnter(index) {
  modal.value = {
    active: true,
    index,
  };
}
function mouseLeave(index) {
  modal.value = {
    active: false,
    index,
  };
}
</script>

<template>
  <main class="flex h-screen items-center justify-center">
    <div class="w-[1000px] flex flex-col items-center justify-center">
      <Project
        @onMouseEnter="mouseEnter"
        @onMouseLeave="mouseLeave"
        v-for="({ title }, index) in projects"
        :key="index"
        :title
        :index
        :modal
      />
    </div>
    <Modal :modal :projects />
  </main>
</template>
