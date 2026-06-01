<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)
const isVisible = ref(false)

const observer = new IntersectionObserver(
  ([entry]) => { isVisible.value = entry.isIntersecting },
  { threshold: 0.15 }
)

onMounted(() => { if (sectionRef.value) observer.observe(sectionRef.value) })
onUnmounted(() => observer.disconnect())
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

      <!-- Content grid -->
      <div
        class="grid grid-cols-1 lg:grid-cols-2 gap-12 lg:gap-16 items-center transition-all duration-700 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <!-- Image -->
        <div class="relative">
          <div class="absolute inset-0 border border-[rgba(200,146,42,0.2)] rounded-sm -translate-x-4 -translate-y-4"></div>
          <div class="relative rounded-sm overflow-hidden aspect-[4/3]">
            <img
              src="/img/Productos.jpeg"
              alt="Productos Ginger Bistro"
              class="w-full h-full object-cover hover:scale-105 transition-transform duration-700"
            />
            <div class="absolute inset-0 bg-gradient-to-r from-[#1a1714]/20 to-transparent"></div>
          </div>

          <!-- Floating label -->
          <div class="absolute top-6 -right-4 bg-[#c8922a] text-[#0d0c0b] font-body font-semibold text-xs tracking-widest uppercase px-4 py-2 rounded-sm">
            Chef's Selection
          </div>
        </div>

        <!-- Text + features -->
        <div>
          <p class="font-body text-[#a89880] text-lg leading-relaxed mb-8">
            Nuestra carta es una celebración de los sabores locales e internacionales,
            elaborados con ingredientes de primera calidad y la pasión de nuestro equipo.
            Desde entrantes creativos hasta postres artesanales, cada plato es una obra
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
            class="inline-flex items-center gap-3 font-body text-sm tracking-widest uppercase px-8 py-3.5 bg-[#c8922a] text-[#0d0c0b] font-medium hover:bg-[#e8b04a] transition-all duration-300 rounded-sm shadow-[0_0_30px_rgba(200,146,42,0.2)] hover:shadow-[0_0_40px_rgba(200,146,42,0.4)] group"
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
