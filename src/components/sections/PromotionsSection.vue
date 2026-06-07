<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface Promo {
  id: number
  src: string
  alt: string
}

const sectionRef = ref<HTMLElement | null>(null)
const isVisible = ref(false)
const currentIndex = ref(0)
const isHovered = ref(false)
let autoplayTimer: number | null = null

const promos: Promo[] = [
  { id: 1, src: '/img/promos/promo1.jpeg', alt: 'Promoción Especial Ginger Bistro 1' },
  { id: 2, src: '/img/promos/promo2.jpeg', alt: 'Promoción Especial Ginger Bistro 2' },
  { id: 3, src: '/img/promos/promo3.jpeg', alt: 'Promoción Especial Ginger Bistro 3' },
  { id: 4, src: '/img/promos/promo4.jpeg', alt: 'Promoción Especial Ginger Bistro 4' },
  { id: 5, src: '/img/promos/promo5.jpeg', alt: 'Promoción Especial Ginger Bistro 5' },
  { id: 6, src: '/img/promos/promo6.jpeg', alt: 'Promoción Especial Ginger Bistro 6' },
  { id: 7, src: '/img/promos/promo7.jpeg', alt: 'Promoción Especial Ginger Bistro 7' }
]

const startAutoplay = () => {
  stopAutoplay()
  autoplayTimer = window.setInterval(() => {
    if (!isHovered.value) {
      nextSlide()
    }
  }, 4000)
}

const stopAutoplay = () => {
  if (autoplayTimer !== null) {
    clearInterval(autoplayTimer)
    autoplayTimer = null
  }
}

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % promos.length
}

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + promos.length) % promos.length
}

const goToSlide = (index: number) => {
  currentIndex.value = index
}

let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      isVisible.value = entry.isIntersecting
    },
    { threshold: 0.1 }
  )
  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
  startAutoplay()
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
  stopAutoplay()
})
</script>

<template>
  <section id="promotions" ref="sectionRef" class="relative py-20 md:py-28 bg-[#0d0c0b] overflow-hidden">
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.4)] to-transparent"></div>

    <!-- Background decoration blob -->
    <div class="absolute -right-40 top-1/2 -translate-y-1/2 w-80 h-80 rounded-full bg-[rgba(200,146,42,0.02)] blur-3xl pointer-events-none"></div>

    <div class="relative z-10 max-w-6xl mx-auto px-6">
      <!-- Section header -->
      <div
        class="text-center mb-12 transition-all duration-700"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <p class="font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] mb-3">Ofertas Especiales</p>
        <h2 class="font-display text-3xl md:text-4xl lg:text-5xl font-light text-[#f5f0e8]">
          Nuestras <em class="italic text-[#c8922a]">Promociones</em>
        </h2>
        <div class="w-12 h-px bg-[#c8922a] mx-auto mt-4"></div>
      </div>

      <!-- Carousel Container -->
      <div
        class="transition-all duration-700 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <div class="relative w-full max-w-4xl mx-auto">
          <!-- Outer border decoration -->
          <div class="absolute inset-0 border border-[rgba(200,146,42,0.15)] rounded-sm -translate-x-3 -translate-y-3 pointer-events-none md:-translate-x-4 md:-translate-y-4"></div>
          
          <!-- Inner frame -->
          <div
            class="relative rounded-sm overflow-hidden aspect-[4/3] sm:aspect-[16/10] md:aspect-[16/9] bg-[#100e0c] shadow-[0_15px_40px_rgba(0,0,0,0.6)] border border-[rgba(200,146,42,0.15)]"
            @mouseenter="isHovered = true"
            @mouseleave="isHovered = false"
          >
            <!-- Transition between slide images -->
            <div class="w-full h-full relative flex items-center justify-center overflow-hidden">
              <Transition
                mode="out-in"
                enter-active-class="transition-all duration-500 ease-out"
                enter-from-class="opacity-0 scale-95"
                enter-to-class="opacity-100 scale-100"
                leave-active-class="transition-all duration-300 ease-in"
                leave-from-class="opacity-100 scale-100"
                leave-to-class="opacity-0 scale-95"
              >
                <div :key="currentIndex" class="w-full h-full relative flex items-center justify-center">
                  <!-- Blurred background copy to fill empty spaces beautifully -->
                  <img
                    :src="promos[currentIndex].src"
                    class="absolute inset-0 w-full h-full object-cover blur-3xl opacity-30 scale-110 pointer-events-none"
                    alt=""
                  />
                  <!-- Sharp centered image with object-contain so it never crops -->
                  <img
                    :src="promos[currentIndex].src"
                    :alt="promos[currentIndex].alt"
                    class="relative max-w-full max-h-full object-contain z-10 shadow-2xl"
                  />
                </div>
              </Transition>
            </div>

            <!-- Gradient overlay for premium cinema look -->
            <div class="absolute inset-0 bg-gradient-to-t from-[#0d0c0b]/50 via-transparent to-[#0d0c0b]/10 pointer-events-none z-10"></div>

            <!-- Controls: Left Arrow -->
            <button
              @click="prevSlide"
              class="absolute left-3 md:left-5 top-1/2 -translate-y-1/2 w-10 h-10 md:w-12 md:h-12 rounded-full border border-[rgba(200,146,42,0.3)] bg-[#0d0c0b]/75 flex items-center justify-center text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300 z-20 group cursor-pointer"
              aria-label="Promoción anterior"
            >
              <svg class="w-4 h-4 md:w-5 md:h-5 transition-transform duration-300 group-hover:-translate-x-0.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
              </svg>
            </button>

            <!-- Controls: Right Arrow -->
            <button
              @click="nextSlide"
              class="absolute right-3 md:right-5 top-1/2 -translate-y-1/2 w-10 h-10 md:w-12 md:h-12 rounded-full border border-[rgba(200,146,42,0.3)] bg-[#0d0c0b]/75 flex items-center justify-center text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300 z-20 group cursor-pointer"
              aria-label="Siguiente promoción"
            >
              <svg class="w-4 h-4 md:w-5 md:h-5 transition-transform duration-300 group-hover:translate-x-0.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
              </svg>
            </button>

            <!-- Floating page counter -->
            <div class="absolute bottom-4 right-4 bg-[#0d0c0b]/80 border border-[rgba(200,146,42,0.2)] px-3 py-1 rounded-sm text-[10px] md:text-xs font-body tracking-widest text-[#e8b04a] z-20">
              {{ currentIndex + 1 }} / {{ promos.length }}
            </div>
          </div>

          <!-- Paging Indicators -->
          <div class="flex justify-center gap-2 mt-6">
            <button
              v-for="(promo, index) in promos"
              :key="promo.id"
              @click="goToSlide(index)"
              class="h-1.5 rounded-full transition-all duration-300 cursor-pointer"
              :class="currentIndex === index ? 'bg-[#c8922a] w-6 md:w-8' : 'bg-gray-700 hover:bg-gray-500 w-1.5 md:w-2'"
              :aria-label="'Ir a la promoción ' + (index + 1)"
            ></button>
          </div>
        </div>
      </div>
    </div>

    <div class="absolute bottom-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.2)] to-transparent"></div>
  </section>
</template>

<style scoped>
</style>
