<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref<HTMLElement | null>(null)
const isVisible = ref(false)

const WHATSAPP_URL = 'https://wa.me/message/LMMFBEAWLY4DH1'

let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      isVisible.value = entry.isIntersecting
    },
    { threshold: 0.15 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<template>
  <section id="contact" ref="sectionRef" class="relative py-28 md:py-36 overflow-hidden bg-[#0d0c0b]">
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.4)] to-transparent"></div>

    <div class="absolute -right-20 bottom-0 w-96 h-96 rounded-full bg-[rgba(200,146,42,0.04)] blur-3xl pointer-events-none"></div>

    <div class="relative z-10 max-w-7xl mx-auto px-6">
      <!-- Header -->
      <div
        class="text-center mb-16 transition-all duration-700"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <p class="font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] mb-4">Estamos aquí para ti</p>
        <h2 class="font-display text-4xl md:text-5xl lg:text-6xl font-light text-[#f5f0e8]">
          <em class="italic text-[#c8922a]">Contacto</em> &amp; Reservas
        </h2>
        <div class="w-12 h-px bg-[#c8922a] mx-auto mt-6"></div>
      </div>

      <div
        class="grid grid-cols-1 lg:grid-cols-2 gap-12 lg:gap-16 items-center transition-all duration-700 delay-200"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
      >
        <!-- Image -->
        <div class="relative order-2 lg:order-1">
          <div class="absolute inset-0 border border-[rgba(200,146,42,0.2)] rounded-sm translate-x-4 translate-y-4"></div>
          <div class="relative rounded-sm overflow-hidden aspect-[4/3]">
            <img
              src="/img/Contactos.jpeg"
              alt="Ginger Bistro contacto"
              class="w-full h-full object-cover hover:scale-105 transition-transform duration-700"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-[#0d0c0b]/40 to-transparent"></div>
          </div>
        </div>

        <!-- Contact info -->
        <div class="order-1 lg:order-2">
          <p class="font-body text-[#a89880] text-lg leading-relaxed mb-10">
            ¿Tienes alguna pregunta, quieres hacer una reserva o simplemente
            deseas saber más sobre nuestra carta? Escríbenos directamente por
            WhatsApp, estamos disponibles para atenderte.
          </p>

          <!-- Contact cards -->
          <div class="space-y-4 mb-10">
            <!-- WhatsApp Card -->
            <a
              :href="WHATSAPP_URL"
              target="_blank"
              rel="noopener noreferrer"
              class="flex items-center gap-5 p-5 border border-[rgba(200,146,42,0.2)] rounded-sm hover:border-[#c8922a] hover:bg-[rgba(200,146,42,0.05)] transition-all duration-300 group cursor-pointer"
              aria-label="Contactar por WhatsApp"
            >
              <div class="flex-shrink-0 w-12 h-12 rounded-full bg-[#25D366]/10 border border-[#25D366]/30 flex items-center justify-center transition-colors duration-300 group-hover:bg-[#25D366]/20">
                <!-- WhatsApp icon SVG -->
                <svg class="w-6 h-6 text-[#25D366]" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
                </svg>
              </div>
              <div>
                <p class="font-body font-medium text-[#f5f0e8] text-sm tracking-wide">WhatsApp</p>
                <p class="font-body text-[#a89880] text-xs mt-0.5">Haz tu reserva ahora</p>
              </div>
              <svg class="w-4 h-4 text-[#c8922a] ml-auto opacity-0 group-hover:opacity-100 transition-all duration-300 group-hover:translate-x-1" viewBox="0 0 16 16" fill="currentColor">
                <path d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
              </svg>
            </a>

            <!-- Location Card -->
            <div class="flex items-center gap-5 p-5 border border-[rgba(200,146,42,0.1)] rounded-sm">
              <div class="flex-shrink-0 w-12 h-12 rounded-full bg-[rgba(200,146,42,0.1)] border border-[rgba(200,146,42,0.2)] flex items-center justify-center">
                <svg class="w-5 h-5 text-[#c8922a]" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z"/>
                  <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z"/>
                </svg>
              </div>
              <div>
                <p class="font-body font-medium text-[#f5f0e8] text-sm tracking-wide">Ubicación</p>
                <p class="font-body text-[#a89880] text-xs mt-0.5">Pamplona, Norte de Santander</p>
              </div>
            </div>

            <!-- Business Hours Card -->
            <div class="flex items-center gap-5 p-5 border border-[rgba(200,146,42,0.1)] rounded-sm">
              <div class="flex-shrink-0 w-12 h-12 rounded-full bg-[rgba(200,146,42,0.1)] border border-[rgba(200,146,42,0.2)] flex items-center justify-center">
                <svg class="w-5 h-5 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
              <div>
                <p class="font-body font-medium text-[#f5f0e8] text-sm tracking-wide">Horario de Atención</p>
                <p class="font-body text-[#a89880] text-xs mt-0.5">Martes a Domingo: 6:00 PM - 10:00 PM</p>
              </div>
            </div>
          </div>

          <!-- Primary CTA -->
          <a
            :href="WHATSAPP_URL"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-3 font-body text-sm tracking-widest uppercase px-8 py-3.5 bg-[#25D366] text-white font-medium hover:bg-[#20bc5a] transition-all duration-300 rounded-sm shadow-[0_0_30px_rgba(37,211,102,0.2)] hover:shadow-[0_0_40px_rgba(37,211,102,0.35)] group cursor-pointer"
          >
            <svg class="w-5 h-5" viewBox="0 0 24 24" fill="currentColor">
              <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
            </svg>
            Escribir por WhatsApp
          </a>
        </div>
      </div>
    </div>

    <div class="absolute bottom-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.2)] to-transparent"></div>
  </section>
</template>
