<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)
const isVisible = ref(false)

const observer = new IntersectionObserver(
  ([entry]) => { isVisible.value = entry.isIntersecting },
  { threshold: 0.1 }
)

onMounted(() => { if (sectionRef.value) observer.observe(sectionRef.value) })
onUnmounted(() => observer.disconnect())
</script>

<template>
  <section ref="sectionRef" class="relative py-20 bg-[#1a1714] overflow-hidden">
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.4)] to-transparent"></div>

    <div
      class="relative z-10 max-w-7xl mx-auto px-6 text-center transition-all duration-700"
      :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
    >
      <p class="font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] mb-4">Encuéntranos</p>
      <h2 class="font-display text-3xl md:text-4xl font-light text-[#f5f0e8] mb-10">
        Nuestra <em class="italic text-[#c8922a]">Ubicación</em>
      </h2>

      <div class="relative rounded-sm overflow-hidden border border-[rgba(200,146,42,0.2)] shadow-2xl">
        <!-- Overlay corners -->
        <div class="absolute top-0 left-0 w-6 h-6 border-t-2 border-l-2 border-[#c8922a] z-10"></div>
        <div class="absolute top-0 right-0 w-6 h-6 border-t-2 border-r-2 border-[#c8922a] z-10"></div>
        <div class="absolute bottom-0 left-0 w-6 h-6 border-b-2 border-l-2 border-[#c8922a] z-10"></div>
        <div class="absolute bottom-0 right-0 w-6 h-6 border-b-2 border-r-2 border-[#c8922a] z-10"></div>

        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3956.7738702661063!2d-72.6520677170008!3d7.379221273627974!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x8e68811119252d73%3A0x88f66067e5b477d1!2sGinger%20Bistro!5e0!3m2!1ses-419!2sco!4v1759122084798!5m2!1ses-419!2sco"
          class="w-full h-80 md:h-[450px] border-0 block"
          loading="lazy"
          allowfullscreen
          referrerpolicy="no-referrer-when-downgrade"
          title="Ubicación Ginger Bistro en Google Maps"
        ></iframe>
      </div>
    </div>
  </section>
</template>
