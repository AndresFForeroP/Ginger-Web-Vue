<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { label: 'Inicio', href: '#hero' },
  { label: 'Nosotros', href: '#about' },
  { label: 'Menú', href: '#menu-digital' },
  { label: 'Contacto', href: '#contact' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const toggleMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMenu = () => {
  isMobileMenuOpen.value = false
}

onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-500"
    :class="isScrolled ? 'bg-[#0d0c0b]/95 backdrop-blur-md shadow-[0_1px_0_rgba(200,146,42,0.2)]' : 'bg-transparent'"
  >
    <nav class="max-w-7xl mx-auto px-8 py-5 flex items-center justify-between">
      <!-- Logo -->
      <a href="#hero" @click="closeMenu" class="flex items-center gap-3 group" aria-label="Ginger Bistro inicio">
        <img
          src="/src/img/LogoGinger.png"
          alt="Ginger Bistro Logo"
          class="h-16 w-auto transition-transform duration-300 group-hover:scale-105"
        />
      </a>

      <!-- Desktop nav -->
      <ul class="hidden md:flex items-center gap-10 font-body" role="list">
        <li v-for="link in navLinks" :key="link.href">
          <a
            :href="link.href"
            class="relative text-sm tracking-widest uppercase text-[#a89880] hover:text-[#e8b04a] transition-colors duration-300 after:absolute after:bottom-[-4px] after:left-0 after:h-px after:w-0 after:bg-[#c8922a] after:transition-all after:duration-300 hover:after:w-full"
          >
            {{ link.label }}
          </a>
        </li>
      </ul>

      <!-- CTA reserva -->
      <a
        href="#contact"
        class="hidden md:inline-flex items-center gap-2 font-body text-sm tracking-wider uppercase px-5 py-2 border border-[#c8922a] text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300 rounded-sm"
      >
        Reservar
      </a>

      <!-- Mobile hamburger -->
      <button
        @click="toggleMenu"
        class="md:hidden flex flex-col gap-1.5 p-2 group"
        :aria-expanded="isMobileMenuOpen"
        aria-label="Abrir menú"
      >
        <span
          class="block h-px w-6 bg-[#f5f0e8] transition-all duration-300"
          :class="isMobileMenuOpen ? 'translate-y-2.5 rotate-45' : ''"
        ></span>
        <span
          class="block h-px w-6 bg-[#f5f0e8] transition-all duration-300"
          :class="isMobileMenuOpen ? 'opacity-0' : ''"
        ></span>
        <span
          class="block h-px w-6 bg-[#f5f0e8] transition-all duration-300"
          :class="isMobileMenuOpen ? '-translate-y-2.5 -rotate-45' : ''"
        ></span>
      </button>
    </nav>

    <!-- Mobile menu -->
    <Transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-2"
    >
      <div
        v-if="isMobileMenuOpen"
        class="md:hidden bg-[#0d0c0b]/98 backdrop-blur-md border-t border-[rgba(200,146,42,0.2)]"
      >
        <ul class="flex flex-col py-6 px-6 gap-6 font-body" role="list">
          <li v-for="link in navLinks" :key="link.href">
            <a
              :href="link.href"
              @click="closeMenu"
              class="block text-sm tracking-widest uppercase text-[#a89880] hover:text-[#e8b04a] transition-colors duration-300"
            >
              {{ link.label }}
            </a>
          </li>
          <li>
            <a
              href="#contact"
              @click="closeMenu"
              class="inline-flex items-center gap-2 font-body text-sm tracking-wider uppercase px-5 py-2 border border-[#c8922a] text-[#c8922a] rounded-sm"
            >
              Reservar
            </a>
          </li>
        </ul>
      </div>
    </Transition>
  </header>
</template>
