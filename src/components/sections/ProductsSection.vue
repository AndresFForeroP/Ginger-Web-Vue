<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

interface ProductImage {
  src: string
  alt: string
  label: string
}

const sectionRef = ref<HTMLElement | null>(null)
const isVisible = ref(false)
const activeIndex = ref(0)
const isHovered = ref(false)
let timer: number | null = null

const productImages: ProductImage[] = [
  { src: '/img/productos/hamburgesas.jpeg', alt: 'Hamburguesas Ginger Bistro', label: 'Burgers Gourmet' },
  { src: '/img/productos/alitas.jpeg', alt: 'Alitas Ginger Bistro', label: 'Alitas de la Casa' },
  { src: '/img/productos/hotdog.jpeg', alt: 'Hot Dogs Ginger Bistro', label: 'Hot Dogs Especiales' }
]

const startTimer = () => {
  stopTimer()
  timer = window.setInterval(() => {
    if (!isHovered.value) {
      nextProduct()
    }
  }, 3500)
}

const stopTimer = () => {
  if (timer !== null) {
    clearInterval(timer)
    timer = null
  }
}

const nextProduct = () => {
  activeIndex.value = (activeIndex.value + 1) % productImages.length
}

const prevProduct = () => {
  activeIndex.value = (activeIndex.value - 1 + productImages.length) % productImages.length
}

let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      isVisible.value = entry.isIntersecting
    },
    { threshold: 0.15 }
  )
  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
  startTimer()
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
  stopTimer()
})
</script>

<template>
  <section id="products" ref="sectionRef" class="relative py-28 md:py-36 bg-[#1a1714] overflow-hidden">
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.4)] to-transparent"></div>

    <!-- Decorative blob -->
    <div class="absolute -left-40 top-1/2 -translate-y-1/2 w-96 h-96 rounded-full bg-[rgba(200,146,42,0.03)] blur-3xl pointer-events-none"></div>

    <div class="relative z-10 max-w-7xl mx-auto px-6">
      <!-- Section header -->
      <div
        class="text-center mb-16 transition-all duration-700"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <p class="font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] mb-4">Lo que ofrecemos</p>
        <h2 class="font-display text-4xl md:text-5xl lg:text-6xl font-light text-[#f5f0e8]">
          Nuestros <em class="italic text-[#c8922a]">Productos</em>
        </h2>
        <div class="w-12 h-px bg-[#c8922a] mx-auto mt-6"></div>
      </div>

      <!-- Content grid - updated to 12 columns for a larger, more prominent layout -->
      <div
        class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center transition-all duration-700 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <!-- Image / Carousel - occupies 7/12 of the space on large screens -->
        <div 
          class="lg:col-span-7 relative w-full"
          @mouseenter="isHovered = true"
          @mouseleave="isHovered = false"
        >
          <!-- Border behind picture frame -->
          <div class="absolute inset-0 border border-[rgba(200,146,42,0.2)] rounded-sm -translate-x-4 -translate-y-4 pointer-events-none"></div>
          
          <!-- Image container -->
          <div class="relative rounded-sm overflow-hidden aspect-[4/3] bg-[#100e0c] border border-[rgba(200,146,42,0.15)] shadow-xl">
            <Transition
              mode="out-in"
              enter-active-class="transition-all duration-500 ease-out"
              enter-from-class="opacity-0 scale-95"
              enter-to-class="opacity-100 scale-100"
              leave-active-class="transition-all duration-300 ease-in"
              leave-from-class="opacity-100 scale-100"
              leave-to-class="opacity-0 scale-95"
            >
              <div :key="activeIndex" class="w-full h-full relative flex items-center justify-center overflow-hidden">
                <!-- Blurred background copy to fill frame space nicely -->
                <img
                  :src="productImages[activeIndex].src"
                  class="absolute inset-0 w-full h-full object-cover blur-3xl opacity-30 scale-110 pointer-events-none"
                  alt=""
                />
                <!-- Sharp centered image with object-contain so it is never cropped -->
                <img
                  :src="productImages[activeIndex].src"
                  :alt="productImages[activeIndex].alt"
                  class="relative max-w-full max-h-full object-contain z-10 shadow-2xl"
                />
              </div>
            </Transition>
            <div class="absolute inset-0 bg-gradient-to-r from-[#1a1714]/10 to-transparent pointer-events-none z-10"></div>

            <!-- Controls: Left Arrow - enlarged for premium control feel -->
            <button
              @click="prevProduct"
              class="absolute left-4 top-1/2 -translate-y-1/2 w-10 h-10 rounded-full border border-[rgba(200,146,42,0.3)] bg-[#0d0c0b]/75 flex items-center justify-center text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300 z-20 cursor-pointer"
              aria-label="Producto anterior"
            >
              <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
              </svg>
            </button>

            <!-- Controls: Right Arrow - enlarged for premium control feel -->
            <button
              @click="nextProduct"
              class="absolute right-4 top-1/2 -translate-y-1/2 w-10 h-10 rounded-full border border-[rgba(200,146,42,0.3)] bg-[#0d0c0b]/75 flex items-center justify-center text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300 z-20 cursor-pointer"
              aria-label="Siguiente producto"
            >
              <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
              </svg>
            </button>

            <!-- Navigation Dots -->
            <div class="absolute bottom-4 left-1/2 -translate-x-1/2 flex gap-2 z-20">
              <button
                v-for="(img, idx) in productImages"
                :key="idx"
                @click="activeIndex = idx"
                class="w-2.5 h-2.5 rounded-full transition-all duration-300 cursor-pointer"
                :class="activeIndex === idx ? 'bg-[#c8922a] w-6' : 'bg-gray-500/70 hover:bg-gray-300'"
                :aria-label="'Ver imagen ' + (idx + 1)"
              ></button>
            </div>
          </div>

          <!-- Floating label - styled with gold gradient and larger size for supreme legibility -->
          <div class="absolute -top-3 -right-3 md:-top-4 md:-right-4 bg-gradient-to-r from-[#c8922a] to-[#d9a33b] text-[#0d0c0b] font-display font-medium text-xs sm:text-sm md:text-base tracking-[0.15em] uppercase px-5 py-2.5 md:px-7 md:py-3.5 rounded-sm shadow-[0_12px_30px_rgba(200,146,42,0.35)] z-20 transition-all duration-500 hover:scale-105 border border-[#e8b04a]/30">
            {{ productImages[activeIndex].label }}
          </div>
        </div>

        <!-- Text + features - occupies 5/12 of the space on large screens -->
        <div class="lg:col-span-5 flex flex-col justify-center">
          <!-- Active Product Name Heading - large, prominent, and animated -->
          <div class="mb-8 border-l-2 border-[#c8922a] pl-4">
            <span class="font-body text-[#c8922a] text-xs tracking-[0.25em] uppercase block mb-1">Producto Seleccionado</span>
            <Transition
              mode="out-in"
              enter-active-class="transition-all duration-300 ease-out"
              enter-from-class="opacity-0 translate-x-2"
              enter-to-class="opacity-100 translate-x-0"
              leave-active-class="transition-all duration-200 ease-in"
              leave-from-class="opacity-100 translate-x-0"
              leave-to-class="opacity-0 -translate-x-2"
            >
              <h3 :key="activeIndex" class="font-display text-3xl md:text-4xl lg:text-5xl font-light text-[#f5f0e8] tracking-wide">
                {{ productImages[activeIndex].label }}
              </h3>
            </Transition>
          </div>

          <p class="font-body text-[#a89880] text-base md:text-lg leading-relaxed mb-8">
            Nuestra carta es una celebración de los sabores locales e internacionales,
            elaborados con ingredientes de primera calidad y la pasión de nuestro equipo.
            Desde entradas creativas hasta hamburguesas Gourmet, cada plato es una obra
            diseñada para sorprenderte.
          </p>

          <!-- Category chips -->
          <div class="flex flex-wrap gap-3 mb-10">
            <span
              v-for="cat in ['Burgers', 'Sándwiches', 'Hot Dogs', 'Alitas & Costillas', 'Bebidas']"
              :key="cat"
              class="font-body text-xs tracking-wider uppercase px-4 py-2 border border-[rgba(200,146,42,0.3)] text-[#c8922a] rounded-sm hover:bg-[rgba(200,146,42,0.1)] transition-colors duration-300 cursor-default"
            >
              {{ cat }}
            </span>
          </div>

          <a
            href="#menu-digital"
            class="inline-flex items-center gap-3 font-body text-sm tracking-widest uppercase px-8 py-3.5 bg-[#c8922a] text-[#0d0c0b] font-medium hover:bg-[#e8b04a] transition-all duration-300 rounded-sm shadow-[0_0_30px_rgba(200,146,42,0.2)] hover:shadow-[0_0_40px_rgba(200,146,42,0.4)] group w-fit"
          >
            Ver Carta Completa
            <svg class="w-4 h-4 transition-transform duration-300 group-hover:translate-x-1" viewBox="0 0 16 16" fill="currentColor">
              <path d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
            </svg>
          </a>
        </div>
      </div>
    </div>

    <div class="absolute bottom-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.2)] to-transparent"></div>
  </section>
</template>

<style scoped>
/* Scoped styles for micro-animations or custom component features if needed */
</style>
