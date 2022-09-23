<template>
  <div
    class="
      hero
      h-[25rem]
      relative
      md:h-[31.25rem]
      after:content-['']
      after:absolute
      after:top-0
      after:left-0
      after:h-full
      after:w-full
      after:bg-fade
    "
  >
    <img
      src="../assets/images/hero_img.png"
      alt=""
      class="w-full h-full object-center bg-fade"
    />
    <div
      class="z-50 absolute top-0 m-0 h-full w-full flex flex-col justify-center"
    >
      <div class="py-0 px-4 w-full max-w-[87.5rem] my-0 mx-auto">
        <span class="font-bold text-lg uppercase text-white mb-8 md:text-2xl">
          <!-- Now Streaming -->
          <h1 class="text-white text-6xl font-extralight mb-2 md:text-7xl">
            <span class="font-medium">Now</span>
            Streaming
          </h1>
          <a class="btn text-xl self-start" href="#movie-grid">View Movies</a>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "hero",
};
</script>

<style lang="scss" scoped>
// .hero{
//   color: #00000099;
// }
</style>
