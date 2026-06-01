<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)
const isVisible = ref(false)

const observer = new IntersectionObserver(
  ([entry]) => { isVisible.value = entry.isIntersecting },
  { threshold: 0.2 }
)

onMounted(() => { if (sectionRef.value) observer.observe(sectionRef.value) })
onUnmounted(() => observer.disconnect())
</script>

<template>
  <section id="about" ref="sectionRef" class="relative py-28 md:py-36 overflow-hidden">
    <!-- Background accent -->
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.4)] to-transparent"></div>
    <div class="absolute inset-0 bg-[#0d0c0b]"></div>

    <!-- Decorative circle -->
    <div class="absolute -right-40 top-1/2 -translate-y-1/2 w-96 h-96 rounded-full bg-[rgba(200,146,42,0.04)] blur-3xl pointer-events-none"></div>

    <div class="relative z-10 max-w-7xl mx-auto px-6">
      <div
        class="grid grid-cols-1 lg:grid-cols-2 gap-16 lg:gap-24 items-center transition-all duration-700"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <!-- Text content -->
        <div>
          <!-- Label -->
          <p class="font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] mb-4">Nuestra Historia</p>

          <h2 class="font-display text-4xl md:text-5xl lg:text-6xl font-light text-[#f5f0e8] leading-tight mb-6">
            Acerca de <br />
            <em class="italic text-[#c8922a]">Ginger Bistro</em>
          </h2>

          <div class="w-12 h-px bg-[#c8922a] mb-8"></div>

          <p class="font-body text-[#a89880] text-lg leading-relaxed mb-6">
            En Ginger Bistro creemos que la buena comida no necesita complicaciones.
            Nuestro concepto de bistronomia fusiona la calidez de un lugar íntimo con
            la excelencia de una cocina de autor, donde cada plato cuenta una historia.
          </p>
          <p class="font-body text-[#a89880] text-lg leading-relaxed mb-10">
            Ubicados en el corazón de Pamplona, Colombia, somos el punto de encuentro para
            quienes buscan sabores auténticos, ambiente acogedor y una experiencia
            gastronómica que queda en la memoria.
          </p>

          <!-- Features -->
          <ul class="grid grid-cols-2 gap-4">
            <li
              v-for="(feat, i) in ['Cocina de autor', 'Ingredientes frescos', 'Ambiente íntimo', 'Experiencia única']"
              :key="i"
              class="flex items-center gap-3 font-body text-sm text-[#f5f0e8]"
            >
              <span class="flex-shrink-0 w-1.5 h-1.5 rounded-full bg-[#c8922a]"></span>
              {{ feat }}
            </li>
          </ul>
        </div>

        <!-- Visual side -->
        <div class="relative">
          <!-- Main decorative element -->
          <div class="relative aspect-[4/5] max-w-md mx-auto lg:mx-0 lg:ml-auto">
            <div class="absolute inset-0 border border-[rgba(200,146,42,0.2)] rounded-sm translate-x-4 translate-y-4"></div>
            <div class="relative h-full rounded-sm overflow-hidden bg-[#1a1714]">
              <img
                src="/img/Fondo1.jpg"
                alt="Ginger Bistro ambiente"
                class="w-full h-full object-cover opacity-80"
              />
              <div class="absolute inset-0 bg-gradient-to-t from-[#0d0c0b]/60 to-transparent"></div>
            </div>

            <!-- Stats floating card -->
            <div class="absolute -bottom-8 left-3 px-10 bg-[#1a1714] border border-[rgba(200,146,42,0.2)] p-6 rounded-sm shadow-2xl">
              <div class="flex gap-8">
                <div class="text-center">
                  <p class="font-display text-3xl font-semibold text-[#c8922a]">+9</p>
                  <p class="font-body text-xs text-[#a89880] tracking-wider uppercase mt-1">Años</p>
                </div>
                <div class="w-px bg-[rgba(200,146,42,0.2)]"></div>
                <div class="text-center">
                  <p class="font-display text-3xl font-semibold text-[#c8922a]">★ 4.7 </p>
                  <p class="font-body text-xs text-[#a89880] tracking-wider uppercase mt-1">Rating Google </p>
                </div>
                <div class="w-px bg-[rgba(200,146,42,0.2)]"></div>
                <div class="text-center">
                  <p class="font-display text-3xl font-semibold text-[#c8922a]">+ 320 </p>
                  <p class="font-body text-xs text-[#a89880] tracking-wider uppercase mt-1">Reseñas </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="absolute bottom-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.2)] to-transparent"></div>
  </section>
</template>
