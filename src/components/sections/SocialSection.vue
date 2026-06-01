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
  <section ref="sectionRef" id="social-media" class="relative py-16 bg-[#0a0908] overflow-hidden">
    <!-- Divider lines -->
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.3)] to-transparent"></div>

    <div class="relative z-10 max-w-5xl mx-auto px-6">
      <div 
        class="bg-[#1a1714] border border-[rgba(200,146,42,0.15)] rounded-sm overflow-hidden shadow-2xl flex flex-col md:flex-row items-center transition-all duration-700"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
      >
        <!-- Left side: image -->
        <div class="w-full md:w-1/2 aspect-[16/10] md:aspect-auto md:h-64 overflow-hidden relative">
          <img 
            src="/img/seccionredes.jpeg" 
            alt="Ginger Bistro Redes Sociales" 
            class="w-full h-full object-cover filter brightness-75 hover:scale-105 transition-transform duration-700"
          />
          <div class="absolute inset-0 bg-gradient-to-r from-transparent via-transparent to-[#1a1714]/80 hidden md:block"></div>
          <div class="absolute inset-0 bg-gradient-to-t from-[#1a1714]/80 via-transparent to-transparent md:hidden"></div>
        </div>

        <!-- Right side: Text and icons -->
        <div class="w-full md:w-1/2 p-8 md:p-12 text-center md:text-left flex flex-col justify-center">
          <p class="font-body text-[10px] tracking-[0.3em] uppercase text-[#c8922a] mb-2">Comunidad Ginger</p>
          <h3 class="font-display text-2xl text-[#f5f0e8] font-light mb-4">
            Síguenos en <em class="italic text-[#c8922a]">Redes</em>
          </h3>
          <p class="font-body text-xs text-[#a89880] leading-relaxed mb-6 max-w-sm">
            Únete a nuestra comunidad para enterarte de nuevos lanzamientos, eventos especiales y más.
          </p>

          <!-- Social Buttons -->
          <div class="flex justify-center md:justify-start gap-4">
            <!-- Instagram -->
            <a 
              href="https://www.instagram.com/gingerbistro/" 
              target="_blank" 
              rel="noopener noreferrer"
              class="w-12 h-12 rounded-full border border-[rgba(200,146,42,0.3)] flex items-center justify-center text-[#a89880] hover:text-[#c8922a] hover:border-[#c8922a] hover:bg-[rgba(200,146,42,0.05)] transition-all duration-300 group"
              aria-label="Sigue a Ginger Bistro en Instagram"
            >
              <svg class="w-5 h-5 group-hover:scale-110 transition-transform" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
              </svg>
            </a>

            <!-- Facebook -->
            <a 
              href="https://www.facebook.com/gingerbistro2017" 
              target="_blank" 
              rel="noopener noreferrer"
              class="w-12 h-12 rounded-full border border-[rgba(200,146,42,0.3)] flex items-center justify-center text-[#a89880] hover:text-[#c8922a] hover:border-[#c8922a] hover:bg-[rgba(200,146,42,0.05)] transition-all duration-300 group"
              aria-label="Sigue a Ginger Bistro en Facebook"
            >
              <svg class="w-5 h-5 group-hover:scale-110 transition-transform" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
                <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
