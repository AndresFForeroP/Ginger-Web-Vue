<script setup>
import { ref } from 'vue'

const activeCategory = ref('burgers')
const showPhysicalMenu = ref(false)
const activePhotoIndex = ref(0)

const menuPhotos = [
  '/src/img/menu1.jpeg',
  '/src/img/menu2.jpeg',
  '/src/img/menu3.jpeg',
  '/src/img/menu4.jpeg'
]

const categories = [
  { 
    id: 'entradas', 
    label: 'Entradas & Adiciones', 
    iconName: 'entradas',
    title: 'Entradas & Adiciones',
    desc: 'El comienzo perfecto o el toque final para tu plato'
  },
  { 
    id: 'burgers', 
    label: 'Burgers', 
    iconName: 'burger',
    title: 'Nuestras Burgers',
    desc: 'Preparadas con pan local y carne premium a la parrilla, acompañadas de papas a la francesa'
  },
  { 
    id: 'sandwiches', 
    label: 'Sándwiches', 
    iconName: 'sandwich',
    title: 'Sándwiches Gourmet',
    desc: 'Con pan local selecto e ingredientes frescos, acompañados de papas a la francesa'
  },
  { 
    id: 'hotdogs', 
    label: 'Hot Dogs', 
    iconName: 'hotdog',
    title: 'Hot Dogs Especiales',
    desc: 'Salchicha americana albardada y queso fundido, acompañados de papas a la francesa'
  },
  { 
    id: 'alitas_costillas', 
    label: 'Alitas & Costillas', 
    iconName: 'alitas',
    title: 'Alitas, Costillas & Quesadillas',
    desc: 'Horneadas lentamente con nuestras salsas glaseadas exclusivas de la casa'
  },
  { 
    id: 'especialidades', 
    label: 'Papitas & Pechugas', 
    iconName: 'especialidades',
    title: 'Especialidades de la Casa',
    desc: 'Las famosas papitas Ginger y deliciosos filetes de pechuga a la parrilla'
  },
  { 
    id: 'bebidas', 
    label: 'Bebidas & Cervezas', 
    iconName: 'bebidas',
    title: 'Bebidas & Cervezas',
    desc: 'Refrescantes opciones para acompañar tu comida excepcional'
  }
]

const menuItems = {
  entradas: {
    items: [
      { name: 'Delicioso Chilli Cremoso', price: '$12.000', desc: 'Acompañado de crujiente guacamole y crujientes nachos artesanales.' },
      { name: 'Trozos de Pechuga Salteada', price: '$12.000', desc: 'En una cremosa salsa BBQ de la casa, acompañado de crujientes nachos y salsa tártara.' }
    ],
    adiciones: [
      { name: 'Carne a la parrilla', price: '$8.000' },
      { name: 'Filete de pollo o trozos de pechuga en BBQ de la casa', price: '$7.000' },
      { name: 'Tocineta de la alemana', price: '$6.000' },
      { name: 'Crocante de parmesano', price: '$6.000' },
      { name: 'Servicio de papas a la francesa', price: '$8.000' }
    ]
  },
  burgers: {
    items: [
      { name: 'Clásica', price: '$18.000', desc: 'Pan local, compota de cebolla, lechuga fresca, carne a la parrilla, queso doble crema, tomate de la casa y salsa tártara.' },
      { name: 'Doble Carne', price: '$25.000', desc: 'Pan local, compota de cebolla, lechuga fresca, doble carne a la parrilla, queso doble crema, tomate de la casa y salsa tártara.' },
      { name: 'Gaucha', price: '$20.000', desc: 'Pan local, chimichurri artesanal, carne a la parrilla, queso doble crema, chorizo de la alemana, tomate de la casa y ricotta fresco de la región.' },
      { name: 'Freddy Mercury', price: '$29.000', desc: 'Pan local, compota de cebolla, lechuga fresca, carne a la parrilla, pechuga a la parrilla, queso doble crema, tocineta crispy, tomate de la casa y mayonesa ahumada.' },
      { name: 'Chilli', price: '$20.000', desc: 'Pan local, guacamole cremoso, carne a la parrilla, queso doble crema, delicioso chilli de la casa, tomate de la casa y salsa tártara.' },
      { name: 'Pesto', price: '$25.000', desc: 'Pan local, compota de cebolla, lechuga fresca, carne a la parrilla, pechuga a la parrilla, queso doble crema, tomate de la casa y nuestra deliciosa mayonesa de pesto.' },
      { name: 'Mixta', price: '$23.000', desc: 'Pan local, compota de cebolla, lechuga fresca, carne a la parrilla, queso doble crema, pollo salteado y reducido en salsa BBQ de la casa, tomate de la casa y salsa tártara.' },
      { name: 'Tocineta Crispy', price: '$23.000', desc: 'Pan local, compota de cebolla, lechuga fresca, carne a la parrilla, queso doble crema, tocineta crispy, tomate de la casa y aderezo de mostaza dulce.' },
      { name: 'Ginger', price: '$26.000', desc: 'Pan local, compota de cebolla, lechuga fresca, carne a la parrilla, queso doble crema, chorizo de la alemana, tocineta crispy y mayonesa de chipotle ligeramente picante.' }
    ]
  },
  sandwiches: {
    items: [
      { name: 'Clásico', price: '$17.000', desc: 'Pan local, compota de cebolla, lechuga fresca, pollo a la parrilla, jamón de la alemana, queso doble crema, tomate de la casa y salsa tártara.' },
      { name: 'Ginger', price: '$21.000', desc: 'Pan local, compota de cebolla, lechuga fresca, pollo a la parrilla, queso doble crema, jamón de la alemana, galleta crujiente de parmesano y mayonesa de pesto.' },
      { name: 'Guacamole', price: '$22.000', desc: 'Pan local, guacamole cremoso, lechuga fresca, pollo a la parrilla, jamón de la alemana, queso doble crema, tocineta crispy, tomate de la casa y salsa tártara.' }
    ]
  },
  hotdogs: {
    items: [
      { name: 'Clásico', price: '$17.000', desc: 'Pan local, mermelada de piña de la casa, papitas fosforito crujientes, salchicha americana seleccionada, salsa tártara y queso doble crema derretido.' },
      { name: 'Chilli', price: '$20.000', desc: 'Pan local, delicioso chilli especiado de la casa, papitas fosforito, salchicha americana albardada, salsa tártara y queso doble crema.' },
      { name: 'Ginger', price: '$20.000', desc: 'Pan local, chimichurri especial, papitas fosforito, pollo salteado reducido en salsa BBQ casera, salchicha americana albardada, salsa tártara y queso doble crema.' },
      { name: 'Crispy', price: '$21.000', desc: 'Pan local, deliciosa mostaza dulce, papitas fosforito, salchicha americana albardada, queso doble crema, rebosado generosamente con tocineta crispy.' }
    ]
  },
  alitas_costillas: {
    items: [
      { name: 'Alitas en BBQ de la casa', price: '$18.000', desc: 'Deliciosas alitas horneadas lentamente y glaseadas en nuestra BBQ secreta hecha en casa.' },
      { name: 'Alitas Lulo & Limonaria', price: '$18.000', desc: 'Deliciosas alitas horneadas lentamente y glaseadas en reducción de lulo con perfume de limonaria.' },
      { name: 'Costillas en BBQ de la casa', price: '$24.000', desc: 'Tiernas costillitas de cerdo horneadas lentamente y glaseadas en nuestra BBQ hecha en casa.' },
      { name: 'Costillas Lulo & Limonaria', price: '$24.000', desc: 'Tiernas costillitas de cerdo horneadas lentamente y glaseadas en reducción de lulo con perfume de limonaria.' },
      { name: 'Quesadillas Pollo BBQ', price: '$18.000', desc: '3 tortillas a la parrilla rellenas de pollo salteado a la cacerola con vegetales en reducción de BBQ y queso doble crema fundido.' },
      { name: 'Quesadillas de Chilli', price: '$18.000', desc: '3 tortillas a la parrilla rellenas de delicioso chilli casero especiado y abundante queso doble crema fundido.' }
    ]
  },
  especialidades: {
    items: [
      { name: 'Papitas Nairo', price: '$23.000', desc: 'Papas a la francesa crujientes, deliciosa mayonesa ahumada, queso doble crema, pollo a la cacerola reducido en BBQ de la casa y coronadas con tocineta crispy.' },
      { name: 'Papitas Egan', price: '$23.000', desc: 'Papas a la francesa crujientes, deliciosa mayonesa ahumada, queso doble crema, pollo a la cacerola reducido en BBQ, chilli de la casa y coronadas con tocineta crispy.' },
      { name: 'Picada Rigo', price: '$44.000', desc: 'Papas a la francesa crujientes, deliciosa mayonesa ahumada, chilli de la casa, pechuga a la parrilla troceada, salchicha americana, queso doble crema y tocineta crispy.' },
      { name: 'Pechuga Clásica', price: '$19.000', desc: 'Filete de pechuga marinada a la parrilla, queso doble crema fundido y jamón de la alemana. Acompañada de papas a la francesa.' },
      { name: 'Pechuga Mostaza Dulce', price: '$23.000', desc: 'Filete de pechuga marinada a la parrilla, queso doble crema, jamón de la alemana, aderezo de mostaza dulce y tocineta crispy. Acompañada de papas a la francesa.' }
    ]
  },
  bebidas: {
    items: [
      { name: 'Bebida Mini', price: '$3.000', desc: 'Presentación mini refrescante.' },
      { name: 'Bebida Personal', price: '$5.000', desc: 'Presentación personal fría.' },
      { name: 'Agua Embotellada', price: '$4.000', desc: 'Agua pura sin gas o con gas.' },
      { name: 'Coca-Cola 1.5L', price: '$10.000', desc: 'Ideal para compartir en mesa.' },
      { name: 'Cuatro 1.5L', price: '$9.000', desc: 'Gaseosa sabor pomelo para compartir.' },
      { name: 'Hit de Litro', price: '$8.000', desc: 'Jugo Hit sabor surtido de litro.' }
    ],
    cervezas: [
      { name: 'Budweiser' },
      { name: 'Club Dorada' },
      { name: 'Poker' },
      { name: 'Corona' },
      { name: 'Coronita' }
    ]
  }
}

const prevPhoto = () => {
  activePhotoIndex.value = (activePhotoIndex.value - 1 + menuPhotos.length) % menuPhotos.length
}

const nextPhoto = () => {
  activePhotoIndex.value = (activePhotoIndex.value + 1) % menuPhotos.length
}
</script>

<template>
  <section id="menu-digital" class="relative py-28 md:py-36 bg-[#0d0c0b] overflow-hidden">
    <!-- Decors -->
    <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[rgba(200,146,42,0.4)] to-transparent"></div>
    <div class="absolute -left-40 top-0 w-96 h-96 rounded-full bg-[rgba(200,146,42,0.03)] blur-3xl pointer-events-none"></div>

    <div class="relative z-10 max-w-6xl mx-auto px-6">
      <!-- Section Title -->
      <div class="text-center mb-16">
        <p class="font-body text-xs tracking-[0.3em] uppercase text-[#c8922a] mb-4">Experiencia Gastronómica</p>
        <h2 class="font-display text-4xl md:text-5xl lg:text-6xl font-light text-[#f5f0e8]">
          Nuestro <em class="italic text-[#c8922a]">Menú</em>
        </h2>
        <div class="w-12 h-px bg-[#c8922a] mx-auto mt-6"></div>
      </div>

      <!-- Action Toggle Buttons -->
      <div class="flex justify-center gap-4 mb-16">
        <button
          @click="showPhysicalMenu = false"
          class="font-body text-xs tracking-widest uppercase px-6 py-3 border rounded-sm transition-all duration-300"
          :class="!showPhysicalMenu ? 'bg-[#c8922a] border-[#c8922a] text-[#0d0c0b] font-medium' : 'border-[rgba(245,240,232,0.2)] text-[#f5f0e8] hover:border-[#c8922a]'"
        >
          Menú Digital
        </button>
        <button
          @click="showPhysicalMenu = true"
          class="font-body text-xs tracking-widest uppercase px-6 py-3 border rounded-sm transition-all duration-300"
          :class="showPhysicalMenu ? 'bg-[#c8922a] border-[#c8922a] text-[#0d0c0b] font-medium' : 'border-[rgba(245,240,232,0.2)] text-[#f5f0e8] hover:border-[#c8922a]'"
        >
          Menú Físico
        </button>
      </div>

      <!-- DIGITAL MENU VIEW -->
      <div v-if="!showPhysicalMenu" class="transition-all duration-500">
        <!-- Category Tabs -->
        <div class="flex flex-wrap justify-center gap-2 md:gap-4 mb-16 border-b border-[rgba(200,146,42,0.15)] pb-6">
          <button
            v-for="cat in categories"
            :key="cat.id"
            @click="activeCategory = cat.id"
            class="flex items-center gap-2 px-4 py-3 rounded-sm font-body text-xs tracking-widest uppercase border transition-all duration-300"
            :class="activeCategory === cat.id ? 'border-[#c8922a] bg-[rgba(200,146,42,0.1)] text-[#e8b04a]' : 'border-transparent text-[#a89880] hover:text-[#f5f0e8]'"
          >
            <!-- Tiny Category SVG Icon -->
            <svg v-if="cat.iconName === 'entradas'" class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 21a9 9 0 0 0 9-9H3a9 9 0 0 0 9 9zM6 12l2-4 2 4M14 12l2-4 2 4" />
            </svg>
            <svg v-else-if="cat.iconName === 'burger'" class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3 10.5C3 6.91 5.91 4 9.5 4h5C18.09 4 21 6.91 21 10.5M21 10.5v1.5a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-1.5M3 13.5c0 2.21 4.03 4 9 4s9-1.79 9-4m-18 2v1.5a3 3 0 0 0 3 3h12a3 3 0 0 0 3-3v-1.5" />
            </svg>
            <svg v-else-if="cat.iconName === 'sandwich'" class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 18h16L12 6 4 18zM4 18v2h16v-2" />
            </svg>
            <svg v-else-if="cat.iconName === 'hotdog'" class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3 13a4 4 0 0 0 4 4h10a4 4 0 0 0 4-4V11a4 4 0 0 0-4-4H7a4 4 0 0 0-4 4v2zM2 12h20" />
            </svg>
            <svg v-else-if="cat.iconName === 'alitas'" class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 3.5c-2.5 0-6.5 2-8 5.5-1.5 3.5-.5 7 2 8s5 0 6.5-3.5 2.5-6.5 2.5-8.5-1-1.5-3-1.5zm-8 13L3.5 20m5.5-1.5L5.5 22.5" />
            </svg>
            <svg v-else-if="cat.iconName === 'especialidades'" class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 8h14l-2 12H7L5 8zm3 0V4m4 4V3m4 5V5" />
            </svg>
            <svg v-else class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18h12M7 18v-8h10v8M9 10V6l4-2v6M17 10h1a2 2 0 0 1 2 2v2a2 2 0 0 1-2 2h-1" />
            </svg>
            {{ cat.label }}
          </button>
        </div>

        <!-- Large Icon and Category Header in active content view -->
        <div class="flex flex-col items-center text-center mb-12">
          <!-- Big Category Icon -->
          <div class="mb-4 p-4 rounded-full bg-[rgba(200,146,42,0.05)] border border-[rgba(200,146,42,0.15)] flex items-center justify-center">
            <!-- Entradas SVG -->
            <svg v-if="activeCategory === 'entradas'" class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 21a9 9 0 0 0 9-9H3a9 9 0 0 0 9 9zM6 12l2-4 2 4M14 12l2-4 2 4" />
            </svg>
            <!-- Burgers SVG -->
            <svg v-else-if="activeCategory === 'burgers'" class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3 10.5C3 6.91 5.91 4 9.5 4h5C18.09 4 21 6.91 21 10.5M21 10.5v1.5a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-1.5M3 13.5c0 2.21 4.03 4 9 4s9-1.79 9-4m-18 2v1.5a3 3 0 0 0 3 3h12a3 3 0 0 0 3-3v-1.5" />
            </svg>
            <!-- Sándwiches SVG -->
            <svg v-else-if="activeCategory === 'sandwiches'" class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 18h16L12 6 4 18zM4 18v2h16v-2" />
            </svg>
            <!-- Hot Dogs SVG -->
            <svg v-else-if="activeCategory === 'hotdogs'" class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M3 13a4 4 0 0 0 4 4h10a4 4 0 0 0 4-4V11a4 4 0 0 0-4-4H7a4 4 0 0 0-4 4v2zM2 12h20" />
            </svg>
            <!-- Alitas/Costillas SVG -->
            <svg v-else-if="activeCategory === 'alitas_costillas'" class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 3.5c-2.5 0-6.5 2-8 5.5-1.5 3.5-.5 7 2 8s5 0 6.5-3.5 2.5-6.5 2.5-8.5-1-1.5-3-1.5zm-8 13L3.5 20m5.5-1.5L5.5 22.5" />
            </svg>
            <!-- Especialidades SVG -->
            <svg v-else-if="activeCategory === 'especialidades'" class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 8h14l-2 12H7L5 8zm3 0V4m4 4V3m4 5V5" />
            </svg>
            <!-- Bebidas SVG -->
            <svg v-else class="w-12 h-12 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18h12M7 18v-8h10v8M9 10V6l4-2v6M17 10h1a2 2 0 0 1 2 2v2a2 2 0 0 1-2 2h-1" />
            </svg>
          </div>
          <h3 class="font-display text-2xl text-[#f5f0e8] font-medium tracking-wide">
            {{ categories.find(c => c.id === activeCategory)?.title }}
          </h3>
          <p class="font-body text-sm text-[#a89880] mt-1 max-w-lg">
            {{ categories.find(c => c.id === activeCategory)?.desc }}
          </p>
        </div>

        <!-- Menu Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-8">
          <div
            v-for="item in menuItems[activeCategory]?.items"
            :key="item.name"
            class="group p-6 bg-[#1a1714]/40 border border-[rgba(200,146,42,0.05)] rounded-sm hover:border-[rgba(200,146,42,0.2)] transition-all duration-300"
          >
            <div class="flex items-baseline justify-between mb-2">
              <h4 class="font-display text-lg text-[#f5f0e8] font-medium group-hover:text-[#e8b04a] transition-colors duration-300">
                {{ item.name }}
              </h4>
              <span class="w-8 h-px bg-[rgba(200,146,42,0.15)] mx-3 grow"></span>
              <span class="font-body text-sm font-semibold text-[#c8922a]">{{ item.price }}</span>
            </div>
            <p v-if="item.desc" class="font-body text-xs text-[#a89880] leading-relaxed mt-2">
              {{ item.desc }}
            </p>
          </div>
        </div>

        <!-- Nested specific items (e.g. Adiciones or Cervezas) -->
        <div v-if="activeCategory === 'entradas' && menuItems.entradas.adiciones" class="mt-16 pt-8 border-t border-[rgba(200,146,42,0.1)]">
          <h4 class="font-display text-xl text-[#f5f0e8] text-center mb-8">Adiciones</h4>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-4xl mx-auto">
            <div
              v-for="addition in menuItems.entradas.adiciones"
              :key="addition.name"
              class="flex justify-between items-center p-4 border border-[rgba(200,146,42,0.05)] bg-[#1a1714]/20 rounded-sm"
            >
              <span class="font-body text-xs text-[#a89880]">✦ {{ addition.name }}</span>
              <span class="font-body text-xs font-semibold text-[#c8922a]">{{ addition.price }}</span>
            </div>
          </div>
        </div>

        <div v-if="activeCategory === 'bebidas' && menuItems.bebidas.cervezas" class="mt-16 pt-8 border-t border-[rgba(200,146,42,0.1)]">
          <h4 class="font-display text-xl text-[#f5f0e8] text-center mb-8">Cervezas Disponibles</h4>
          <div class="flex flex-wrap justify-center gap-4 max-w-3xl mx-auto">
            <span
              v-for="beer in menuItems.bebidas.cervezas"
              :key="beer.name"
              class="font-body text-xs tracking-wider uppercase px-4 py-2 bg-[#1a1714] border border-[rgba(200,146,42,0.15)] text-[#a89880] rounded-sm"
            >
              🍺 {{ beer.name }}
            </span>
          </div>
        </div>
      </div>

      <!-- PHYSICAL MENU GALLERY VIEW -->
      <div v-else class="transition-all duration-500">
        <div class="relative max-w-xl mx-auto border border-[rgba(200,146,42,0.2)] rounded-sm overflow-hidden bg-[#1a1714]">
          <!-- Top corners decoration -->
          <div class="absolute top-0 left-0 w-4 h-4 border-t-2 border-l-2 border-[#c8922a] z-10"></div>
          <div class="absolute top-0 right-0 w-4 h-4 border-t-2 border-r-2 border-[#c8922a] z-10"></div>

          <!-- Carousel Container with sliding animation -->
          <div class="relative aspect-[3/4] flex items-center justify-center overflow-hidden">
            <Transition
              mode="out-in"
              enter-active-class="transition-all duration-300 ease-out"
              enter-from-class="opacity-0 scale-95"
              enter-to-class="opacity-100 scale-100"
              leave-active-class="transition-all duration-200 ease-in"
              leave-from-class="opacity-100 scale-100"
              leave-to-class="opacity-0 scale-95"
            >
              <img
                :key="activePhotoIndex"
                :src="menuPhotos[activePhotoIndex]"
                alt="Página de Menú Físico"
                class="w-full h-full object-contain"
              />
            </Transition>
          </div>

          <!-- Navigation controls overlay -->
          <div class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-black/90 to-transparent p-6 flex items-center justify-between">
            <button
              @click="prevPhoto"
              class="w-10 h-10 rounded-full border border-[rgba(200,146,42,0.3)] flex items-center justify-center text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300"
              aria-label="Foto anterior"
            >
              ←
            </button>
            <span class="font-body text-xs tracking-widest text-[#a89880]">
              Página {{ activePhotoIndex + 1 }} de {{ menuPhotos.length }}
            </span>
            <button
              @click="nextPhoto"
              class="w-10 h-10 rounded-full border border-[rgba(200,146,42,0.3)] flex items-center justify-center text-[#c8922a] hover:bg-[#c8922a] hover:text-[#0d0c0b] transition-all duration-300"
              aria-label="Siguiente foto"
            >
              →
            </button>
          </div>
        </div>

        <!-- Dot Indicators for easy navigation -->
        <div class="flex justify-center gap-2 mt-6">
          <button
            v-for="(photo, index) in menuPhotos"
            :key="index"
            @click="activePhotoIndex = index"
            class="w-2.5 h-2.5 rounded-full transition-all duration-300"
            :class="activePhotoIndex === index ? 'bg-[#c8922a] w-6' : 'bg-gray-700 hover:bg-gray-500'"
            :aria-label="'Ir a página ' + (index + 1)"
          ></button>
        </div>
      </div>

      <!-- Menu date / Status bottom -->
      <div class="text-center mt-20">
        <p class="font-body text-xs tracking-widest text-[#a89880]/60">
          ✨ Menú digital e impreso actualizado al 2026
        </p>
      </div>

    </div>
  </section>
</template>
