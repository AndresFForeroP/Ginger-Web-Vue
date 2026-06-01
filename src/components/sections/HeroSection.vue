<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => { isVisible.value = true }, 100)
})
</script>

<template>
  <section id="hero" class="relative min-h-screen flex items-center justify-center overflow-hidden">
    <!-- Background image with opacity and initial zoom-out animation -->
    <div
      class="absolute inset-0 bg-cover bg-[center_20%] bg-no-repeat opacity-45 "
      style="background-image: url('/src/img/Fondo1.jpg')"
    ></div>

    <!-- Gradient overlays for cinematic effect -->
    <div class="absolute inset-0 bg-gradient-to-b from-[#0d0c0b]/80 via-[#0d0c0b]/40 to-[#0d0c0b]"></div>
    <div class="absolute inset-0 bg-gradient-to-r from-[#0d0c0b]/70 via-transparent to-[#0d0c0b]/40"></div>

    <!-- Subtle grain texture overlay -->
    <div class="absolute inset-0 opacity-[0.03]" style="background-image: url('data:image/svg+xml,%3Csvg viewBox=%220 0 200 200%22 xmlns=%22http://www.w3.org/2000/svg%22%3E%3Cfilter id=%22n%22%3E%3CfeTurbulence type=%22fractalNoise%22 baseFrequency=%221%22 numOctaves=%224%22/%3E%3C/filter%3E%3Crect width=%22100%25%22 height=%22100%25%22 filter=%22url(%23n)%22/%3E%3C/svg%3E'); background-size: 200px 200px;"></div>

    <!-- Content -->
    <div
      class="relative z-10 text-center px-6 max-w-4xl mx-auto transition-all duration-1000"
      :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
    >
      <!-- Badge -->
      <div class="inline-flex items-center gap-2 mb-8 font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] border border-[rgba(200,146,42,0.3)] px-4 py-2 rounded-sm">
        <span class="w-1.5 h-1.5 rounded-full bg-[#c8922a] animate-pulse"></span>
        Bistronomia · Pamplona, Colombia
      </div>

      <!-- Logo with glow -->
      <div class="flex justify-center mb-8">
        <img
          src="/src/img/LogoGinger.png"
          alt="Ginger Bistro"
          class="h-28 md:h-36 w-auto drop-shadow-[0_0_20px_rgba(200,146,42,0.25)] transition-all duration-700 hover:scale-105"
        />
      </div>

      <!-- Headline -->
      <h1 class="font-display text-5xl md:text-7xl lg:text-8xl font-light text-[#f5f0e8] leading-[0.9] tracking-tight mb-4 shimmer-text">
        Lugar <em class="italic text-[#c8922a]">sencillo</em>,
        <br />
        <span class="font-semibold">comida excepcional</span>
      </h1>

      <!-- Subtitle -->
      <p class="font-body font-light text-lg md:text-xl text-[#a89880] mt-6 mb-10 tracking-wide">
        Vive la experiencia · Descubre nuestros sabores únicos
      </p>

      <!-- CTAs -->
      <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
        <a
          href="#menu-digital"
          class="font-body text-sm tracking-widest uppercase px-8 py-3.5 bg-[#c8922a] text-[#0d0c0b] font-medium hover:bg-[#e8b04a] transition-all duration-300 rounded-sm shadow-[0_0_30px_rgba(200,146,42,0.3)] hover:shadow-[0_0_40px_rgba(200,146,42,0.5)]"
        >
          Ver Menú
        </a>
        <a
          href="#about"
          class="font-body text-sm tracking-widest uppercase px-8 py-3.5 border border-[rgba(245,240,232,0.3)] text-[#f5f0e8] hover:border-[#c8922a] hover:text-[#c8922a] transition-all duration-300 rounded-sm"
        >
          Conocernos
        </a>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 animate-bounce">
      <span class="font-body text-[10px] tracking-[0.3em] uppercase text-[#a89880]">Scroll</span>
      <div class="w-px h-8 bg-gradient-to-b from-[#c8922a] to-transparent"></div>
    </div>
  </section>
</template>

<style scoped>
@keyframes zoomBackground {
  0% {
    transform: scale(1.15);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes shimmerGold {
  0%, 100% {
    text-shadow: 0 0 10px rgba(200, 146, 42, 0);
  }
  50% {
    text-shadow: 0 0 25px rgba(200, 146, 42, 0.3);
  }
}
.zoom-bg {
  animation: zoomBackground 8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
.shimmer-text {
  animation: shimmerGold 5s ease-in-out infinite;
}
</style>
