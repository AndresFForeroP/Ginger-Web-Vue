<script setup>
import { ref } from 'vue'

const activeCategory = ref('entradas')
const showPhysicalMenu = ref(false)
const activePhotoIndex = ref(0)

const menuPhotos = [
  '/src/img/menu1.jpeg',
  '/src/img/menu2.jpeg',
  '/src/img/menu3.jpeg',
  '/src/img/menu4.jpeg'
]

const categories = [
  { id: 'entradas', label: 'Entradas', icon: 'M12 3v18M3 12h18' }, // Plus/Cross or custom plates
  { id: 'fuertes', label: 'Platos Fuertes', icon: 'M12 2a10 10 0 1 0 10 10A10 10 0 0 0 12 2zm1 11H11v-4h2z' }, // Plate representation
  { id: 'postres', label: 'Postres', icon: 'M12 3c-4.97 0-9 4.03-9 9 0 2.12.74 4.07 1.97 5.61L12 21l7.03-3.39c1.23-1.54 1.97-3.49 1.97-5.61 0-4.97-4.03-9-9-9z' }, // Ice cream / Sweet
  { id: 'bebidas', label: 'Bebidas', icon: 'M19 8h-1V3H6v5H5a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V10a2 2 0 0 0-2-2zM8 5h8v3H8V5z' } // Cup/Glass
]

const menuItems = {
  entradas: [
    { name: 'Bruschetta Rústica', price: '$18.000', desc: 'Pan artesanal de masa madre tostado, tomates confitados al romero, pesto de albahaca fresca y lascas de queso parmesano.' },
    { name: 'Carpaccio de Lomo de Res', price: '$26.000', desc: 'Finas láminas de lomo sellado, aderezadas con vinagreta de limón, alcaparras bebés, rúgula silvestre y virutas de queso maduro.' },
    { name: 'Champiñones Gratinados', price: '$20.000', desc: 'Champiñones de París rellenos de una mezcla de quesos finos y hierbas aromáticas, fundidos al horno.' },
    { name: 'Ceviche Ginger', price: '$28.000', desc: 'Ceviche clásico de pescado blanco con leche de tigre infusionada con jengibre fresco, cilantro y maíz tierno.' }
  ],
  fuertes: [
    { name: 'Lomo en Costra de Pimienta', price: '$48.000', desc: 'Medallón de lomo premium en costra de pimientas seleccionadas, salsa demi-glace, acompañado de puré rústico trufado.' },
    { name: 'Salmón Glaseado', price: '$46.000', desc: 'Filete de salmón a la plancha con un sutil glaseado de jengibre y miel de Pamplona, sobre cama de vegetales crujientes.' },
    { name: 'Risotto de Setas & Trufa', price: '$38.000', desc: 'Arroz arborio cocido lentamente en caldo de hongos frescos, mantequilla de trufa negra y queso Grana Padano.' },
    { name: 'Fettuccine Frutti di Mare', price: '$42.000', desc: 'Pasta artesanal salteada al wok con calamares, camarones y mejillones en salsa pomodoro rústica y albahaca.' }
  ],
  postres: [
    { name: 'Volcán de Chocolate', price: '$16.000', desc: 'Torta húmeda de chocolate oscuro con corazón fundido y caliente, acompañado de helado artesanal de vainilla.' },
    { name: 'Cheesecake de Frutos Rojos', price: '$15.000', desc: 'Base crujiente de galletas de almendra con crema suave de queso de la región y coulis artesanal de frutos del bosque.' },
    { name: 'Crème Brûlée de Jengibre', price: '$14.000', desc: 'Crema cocida clásica con un toque aromático de jengibre y una costra crujiente de azúcar caramelizada.' }
  ],
  bebidas: [
    { name: 'Limonada de Coco & Jengibre', price: '$12.000', desc: 'Bebida ultra refrescante licuada con pulpa de coco natural y un toque especial de jengibre.' },
    { name: 'Gin Tonic Bistro', price: '$26.000', desc: 'Ginebra seleccionada, agua tónica premium, frutos rojos silvestres deshidratados y una rama de romero ahumado.' },
    { name: 'Soda de Frutos Amarillos', price: '$10.000', desc: 'Soda artesanal preparada con almíbar casero de maracuyá, mango y piña.' },
    { name: 'Copa de Vino de la Casa', price: '$18.000', desc: 'Tinto o blanco especialmente seleccionado para maridar con nuestros platos.' }
  ]
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
      <div class="flex justify-center gap-4 mb-12">
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
          Ver Menú Físico (Fotos)
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
            class="flex items-center gap-2 px-5 py-3 rounded-sm font-body text-xs tracking-widest uppercase border transition-all duration-300"
            :class="activeCategory === cat.id ? 'border-[#c8922a] bg-[rgba(200,146,42,0.1)] text-[#e8b04a]' : 'border-transparent text-[#a89880] hover:text-[#f5f0e8]'"
          >
            <!-- SVG Icon helper dynamically drawn -->
            <svg class="w-4 h-4 text-[#c8922a]" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" :d="cat.icon" />
            </svg>
            {{ cat.label }}
          </button>
        </div>

        <!-- Menu Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-10">
          <div
            v-for="item in menuItems[activeCategory]"
            :key="item.name"
            class="group p-6 bg-[#1a1714]/40 border border-[rgba(200,146,42,0.05)] rounded-sm hover:border-[rgba(200,146,42,0.2)] transition-all duration-300"
          >
            <div class="flex items-baseline justify-between mb-2">
              <h3 class="font-display text-xl text-[#f5f0e8] font-medium group-hover:text-[#e8b04a] transition-colors duration-300">
                {{ item.name }}
              </h3>
              <span class="w-12 h-px bg-[rgba(200,146,42,0.2)] mx-4 grow"></span>
              <span class="font-body text-sm font-semibold text-[#c8922a]">{{ item.price }}</span>
            </div>
            <p class="font-body text-xs text-[#a89880] leading-relaxed mt-2">
              {{ item.desc }}
            </p>
          </div>
        </div>
      </div>

      <!-- PHYSICAL MENU GALLERY VIEW -->
      <div v-else class="transition-all duration-500">
        <div class="relative max-w-xl mx-auto border border-[rgba(200,146,42,0.2)] rounded-sm overflow-hidden bg-[#1a1714]">
          <!-- Top corners decoration -->
          <div class="absolute top-0 left-0 w-4 h-4 border-t-2 border-l-2 border-[#c8922a] z-10"></div>
          <div class="absolute top-0 right-0 w-4 h-4 border-t-2 border-r-2 border-[#c8922a] z-10"></div>

          <!-- Carousel Container -->
          <div class="relative aspect-[3/4] flex items-center justify-center">
            <img
              :src="menuPhotos[activePhotoIndex]"
              alt="Página de Menú Físico"
              class="w-full h-full object-contain"
            />
          </div>

          <!-- Navigation controls overlay -->
          <div class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-black/80 to-transparent p-6 flex items-center justify-between">
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
      </div>

      <!-- Menu date / Status bottom -->
      <div class="text-center mt-16">
        <p class="font-body text-xs tracking-widest text-[#a89880]/60">
          ✨ Menú digital e impreso actualizado al 2026
        </p>
      </div>

    </div>
  </section>
</template>
