<template>
  <section class="image-carousel-section">
    <div class="container">
      <div class="carousel-header">
        <h2 class="carousel-title">NUESTRA<br><span class="highlight-text">GALERÍA</span></h2>
        <p class="carousel-subtitle">Descubre la experiencia Chicken Rise</p>
      </div>
      
      <div class="carousel-container">
        <div class="carousel-wrapper" ref="carouselWrapper">
          <div 
            class="carousel-track" 
            ref="carouselTrack"
            :style="{ transform: `translateX(-${currentSlide * slideWidth}px)` }"
          >
            <div 
              v-for="(image, index) in images" 
              :key="index" 
              class="carousel-slide"
              :class="{ 'active': index === currentSlide }"
            >
              <div class="image-container" @click="openModal(image, index)">
                <img 
                  :src="image.src" 
                  :alt="image.alt" 
                  class="carousel-image"
                  @load="handleImageLoad"
                  @error="handleImageError"
                >
                <div class="image-overlay">
                  <div class="overlay-content">
                    <h4 class="image-title">{{ image.title }}</h4>
                    <p class="image-description">{{ image.description }}</p>
                    <div class="click-indicator">
                      <i class="fas fa-expand-alt"></i>
                      <span>Click para ampliar</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Controles de navegación -->
        <button 
          class="carousel-btn prev-btn" 
          @click="prevSlide"
          v-show="images.length > 1"
        >
          <i class="fas fa-chevron-left"></i>
        </button>
        
        <button 
          class="carousel-btn next-btn" 
          @click="nextSlide"
          v-show="images.length > 1"
        >
          <i class="fas fa-chevron-right"></i>
        </button>
        
        <!-- Indicadores -->
        <div class="carousel-indicators">
          <button
            v-for="(image, index) in images"
            :key="index"
            class="indicator"
            :class="{ 'active': index === currentSlide }"
            @click="goToSlide(index)"
          ></button>
        </div>
      </div>
    </div>
    
    <!-- Modal para imagen ampliada -->
    <div 
      v-if="showModal" 
      class="image-modal" 
      @click="closeModal"
      @keydown.esc="closeModal"
    >
      <div class="modal-content" @click.stop>
        <button class="modal-close" @click="closeModal">
          <i class="fas fa-times"></i>
        </button>
        
        <div class="modal-image-container">
          <img 
            :src="modalImage.src" 
            :alt="modalImage.alt" 
            class="modal-image"
          >
        </div>
        
        <div class="modal-info">
          <h3 class="modal-title">{{ modalImage.title }}</h3>
          <p class="modal-description">{{ modalImage.description }}</p>
        </div>
        
        <!-- Navegación en modal -->
        <button 
          class="modal-nav prev-modal" 
          @click="prevModalImage"
          v-show="images.length > 1"
        >
          <i class="fas fa-chevron-left"></i>
        </button>
        
        <button 
          class="modal-nav next-modal" 
          @click="nextModalImage"
          v-show="images.length > 1"
        >
          <i class="fas fa-chevron-right"></i>
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

// Datos de imágenes (puedes personalizar estas)
const images = ref([
  {
    src: '/burger-menu.png',
    alt: 'Menú Burger Chicken Rise',
    title: 'Nuestras Hamburguesas',
    description: 'Deliciosas hamburguesas de pollo halal'
  },
  {
    src: '/menu-pollo.png',
    alt: 'Menú Pollo Chicken Rise',
    title: 'Pollo Halal Premium',
    description: 'La mejor calidad garantizada'
  },
  {
    src: '/glovo.png',
    alt: 'Delivery Service',
    title: 'Servicio de Delivery',
    description: 'Llevamos el sabor a tu hogar'
  },
  {
    src: '/hero-bg.png',
    alt: 'Restaurante Chicken Rise',
    title: 'Nuestro Restaurante',
    description: 'Ambiente acogedor y familiar'
  },
  {
    src: '/logo-bg.png',
    alt: 'Logo Chicken Rise',
    title: 'Chicken Rise',
    description: 'Mucho más que pollo'
  }
])

// Variables reactivas
const currentSlide = ref(0)
const slideWidth = ref(300)
const carouselWrapper = ref(null)
const carouselTrack = ref(null)
const autoplayInterval = ref(null)
const isAutoplay = ref(true)

// Variables para el modal
const showModal = ref(false)
const modalImage = ref({})
const currentModalIndex = ref(0)

// Computed
const maxSlide = computed(() => Math.max(0, images.value.length - getSlidesPerView()))

// Métodos
const getSlidesPerView = () => {
  if (!window) return 1
  if (window.innerWidth >= 1200) return 3
  if (window.innerWidth >= 768) return 2
  return 1
}

const updateSlideWidth = () => {
  if (carouselWrapper.value) {
    const containerWidth = carouselWrapper.value.offsetWidth
    const slidesPerView = getSlidesPerView()
    slideWidth.value = Math.floor(containerWidth / slidesPerView)
  }
}

const nextSlide = () => {
  if (currentSlide.value < maxSlide.value) {
    currentSlide.value++
  } else {
    currentSlide.value = 0 // Loop back to start
  }
}

const prevSlide = () => {
  if (currentSlide.value > 0) {
    currentSlide.value--
  } else {
    currentSlide.value = maxSlide.value // Loop to end
  }
}

const goToSlide = (index) => {
  currentSlide.value = Math.min(index, maxSlide.value)
}

const handleImageLoad = () => {
  updateSlideWidth()
}

const handleImageError = (event) => {
  // Imagen de fallback si no se puede cargar
  event.target.src = 'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjMwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiBmaWxsPSIjZGRkIi8+PHRleHQgeD0iNTAlIiB5PSI1MCUiIGZvbnQtZmFtaWx5PSJBcmlhbCwgc2Fucy1zZXJpZiIgZm9udC1zaXplPSIxOCIgZmlsbD0iIzk5OSIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZHk9Ii4zZW0iPkltYWdlbiBubyBkaXNwb25ibGU8L3RleHQ+PC9zdmc+'
}

const startAutoplay = () => {
  if (isAutoplay.value) {
    autoplayInterval.value = setInterval(() => {
      nextSlide()
    }, 4000)
  }
}

const stopAutoplay = () => {
  if (autoplayInterval.value) {
    clearInterval(autoplayInterval.value)
    autoplayInterval.value = null
  }
}

const handleResize = () => {
  updateSlideWidth()
  currentSlide.value = Math.min(currentSlide.value, maxSlide.value)
}

// Métodos del modal
const openModal = (image, index) => {
  modalImage.value = image
  currentModalIndex.value = index
  showModal.value = true
  stopAutoplay() // Parar autoplay cuando el modal está abierto
  document.body.style.overflow = 'hidden' // Prevenir scroll del body
}

const closeModal = () => {
  showModal.value = false
  modalImage.value = {}
  document.body.style.overflow = 'auto' // Restaurar scroll del body
  if (isAutoplay.value) {
    startAutoplay() // Reanudar autoplay
  }
}

const nextModalImage = () => {
  const nextIndex = (currentModalIndex.value + 1) % images.value.length
  modalImage.value = images.value[nextIndex]
  currentModalIndex.value = nextIndex
}

const prevModalImage = () => {
  const prevIndex = currentModalIndex.value === 0 
    ? images.value.length - 1 
    : currentModalIndex.value - 1
  modalImage.value = images.value[prevIndex]
  currentModalIndex.value = prevIndex
}

// Manejo de teclas
const handleKeydown = (event) => {
  if (!showModal.value) return
  
  switch (event.key) {
    case 'Escape':
      closeModal()
      break
    case 'ArrowRight':
      nextModalImage()
      break
    case 'ArrowLeft':
      prevModalImage()
      break
  }
}

// Lifecycle
onMounted(() => {
  // Pequeño delay para asegurar que el DOM está completamente renderizado
  setTimeout(() => {
    updateSlideWidth()
    startAutoplay()
  }, 100)
  
  window.addEventListener('resize', handleResize)
  document.addEventListener('keydown', handleKeydown)
  
  // Intersection Observer para animaciones
  const observerOptions = {
    threshold: 0.2,
    rootMargin: '0px 0px -50px 0px'
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
      }
    })
  }, observerOptions)

  const carouselHeader = document.querySelector('.carousel-header')
  const carouselContainer = document.querySelector('.carousel-container')
  
  if (carouselHeader) observer.observe(carouselHeader)
  if (carouselContainer) observer.observe(carouselContainer)
})

onUnmounted(() => {
  stopAutoplay()
  window.removeEventListener('resize', handleResize)
  document.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = 'auto' // Asegurar que el scroll se restaure
})
</script>

<style scoped>
.image-carousel-section {
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 50%, #1a1a1a 100%);
  padding: 6rem 0;
  position: relative;
  overflow: hidden;
}

.image-carousel-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle at 20% 80%, rgba(220, 53, 69, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(255, 193, 7, 0.1) 0%, transparent 50%),
    linear-gradient(45deg, transparent 48%, rgba(255, 255, 255, 0.02) 49%, rgba(255, 255, 255, 0.02) 51%, transparent 52%);
  pointer-events: none;
}

.container {
  position: relative;
  z-index: 2;
}

/* Header */
.carousel-header {
  text-align: center;
  margin-bottom: 4rem;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease;
}

.carousel-header.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.carousel-title {
  font-family: 'Inter', sans-serif;
  font-size: clamp(2.5rem, 4vw, 3.5rem);
  font-weight: 900;
  color: #f8f9fa;
  text-transform: uppercase;
  letter-spacing: 3px;
  margin-bottom: 1rem;
  position: relative;
  line-height: 1.1;
}

.highlight-text {
  color: #dc3545;
  display: block;
  font-weight: 900;
  margin-top: 0.5rem;
}

.carousel-title::after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #dc3545, #ffc107);
  border-radius: 2px;
}

.carousel-subtitle {
  font-size: 1.2rem;
  color: #ced4da;
  margin-top: 2rem;
  font-style: italic;
}

/* Carousel */
.carousel-container {
  position: relative;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease 0.3s;
}

.carousel-container.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.carousel-wrapper {
  overflow: hidden;
  border-radius: 20px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.carousel-track {
  display: flex;
  transition: transform 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.carousel-slide {
  flex-shrink: 0;
  padding: 0 10px;
  box-sizing: border-box;
  transition: all 0.6s ease;
}

/* Responsive slide widths */
@media (min-width: 1200px) {
  .carousel-slide {
    width: calc(100% / 3);
  }
}

@media (min-width: 768px) and (max-width: 1199px) {
  .carousel-slide {
    width: calc(100% / 2);
  }
}

@media (max-width: 767px) {
  .carousel-slide {
    width: 100%;
  }
}

.image-container {
  position: relative;
  border-radius: 15px;
  overflow: hidden;
  aspect-ratio: 4/3;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  cursor: pointer;
  transition: transform 0.3s ease;
}

.image-container:hover {
  transform: scale(1.02);
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: all 0.5s ease;
  filter: brightness(0.9) contrast(1.1);
}

.image-container:hover .carousel-image {
  transform: scale(1.1);
  filter: brightness(1) contrast(1.2);
}

.image-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(
    to top,
    rgba(0, 0, 0, 0.8) 0%,
    rgba(0, 0, 0, 0.4) 50%,
    transparent 100%
  );
  color: white;
  padding: 2rem 1.5rem 1.5rem;
  transform: translateY(20px);
  opacity: 0;
  transition: all 0.3s ease;
}

.image-container:hover .image-overlay {
  transform: translateY(0);
  opacity: 1;
}

.image-title {
  font-size: 1.3rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #ffc107;
}

.image-description {
  font-size: 0.95rem;
  color: #e9ecef;
  margin: 0 0 1rem 0;
  line-height: 1.4;
}

.click-indicator {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: #ffc107;
  font-weight: 600;
}

.click-indicator i {
  font-size: 1rem;
}

/* Controles */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(220, 53, 69, 0.9);
  color: white;
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 3;
  backdrop-filter: blur(5px);
}

.carousel-btn:hover:not(:disabled) {
  background: rgba(220, 53, 69, 1);
  transform: translateY(-50%) scale(1.1);
  box-shadow: 0 5px 15px rgba(220, 53, 69, 0.4);
}

.carousel-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.prev-btn {
  left: 20px;
}

.next-btn {
  right: 20px;
}

/* Indicadores */
.carousel-indicators {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 2rem;
}

.indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
}

.indicator.active {
  background: #dc3545;
  transform: scale(1.2);
}

.indicator:hover {
  background: rgba(255, 255, 255, 0.6);
}

/* Modal Styles */
.image-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.95);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  backdrop-filter: blur(5px);
  animation: modalFadeIn 0.3s ease-out;
}

@keyframes modalFadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.modal-content {
  position: relative;
  max-width: 90vw;
  max-height: 90vh;
  background: #1a1a1a;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
  animation: modalSlideIn 0.3s ease-out;
}

@keyframes modalSlideIn {
  from {
    transform: scale(0.8) translateY(50px);
    opacity: 0;
  }
  to {
    transform: scale(1) translateY(0);
    opacity: 1;
  }
}

.modal-close {
  position: absolute;
  top: 20px;
  right: 20px;
  background: rgba(220, 53, 69, 0.9);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 1.2rem;
  cursor: pointer;
  z-index: 10;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}

.modal-close:hover {
  background: rgba(220, 53, 69, 1);
  transform: scale(1.1);
}

.modal-image-container {
  width: 100%;
  height: 70vh;
  max-height: 600px;
  overflow: hidden;
}

.modal-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  object-position: center;
}

.modal-info {
  padding: 2rem;
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
  text-align: center;
}

.modal-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffc107;
  margin-bottom: 1rem;
  font-family: 'Inter', sans-serif;
}

.modal-description {
  font-size: 1.1rem;
  color: #e9ecef;
  line-height: 1.6;
  margin: 0;
}

.modal-nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(220, 53, 69, 0.9);
  color: white;
  border: none;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  font-size: 1.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}

.modal-nav:hover {
  background: rgba(220, 53, 69, 1);
  transform: translateY(-50%) scale(1.1);
}

.prev-modal {
  left: 20px;
}

.next-modal {
  right: 20px;
}

/* Responsive */
@media (max-width: 768px) {
  .image-carousel-section {
    padding: 4rem 0;
  }
  
  .carousel-header {
    margin-bottom: 3rem;
  }
  
  .carousel-title {
    font-size: 2rem;
    letter-spacing: 2px;
  }
  
  .carousel-subtitle {
    font-size: 1rem;
  }
  
  .carousel-btn {
    width: 40px;
    height: 40px;
    font-size: 1rem;
  }
  
  .prev-btn {
    left: 10px;
  }
  
  .next-btn {
    right: 10px;
  }
  
  .image-overlay {
    padding: 1.5rem 1rem 1rem;
  }
  
  .image-title {
    font-size: 1.1rem;
  }
  
  .image-description {
    font-size: 0.85rem;
  }
}

@media (max-width: 576px) {
  .image-carousel-section {
    padding: 3rem 0;
  }
  
  .carousel-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
  }
  
  .carousel-subtitle {
    font-size: 0.9rem;
  }
  
  /* Modal responsive */
  .modal-content {
    max-width: 95vw;
    max-height: 95vh;
  }
  
  .modal-image-container {
    height: 60vh;
  }
  
  .modal-info {
    padding: 1.5rem;
  }
  
  .modal-title {
    font-size: 1.4rem;
  }
  
  .modal-description {
    font-size: 1rem;
  }
  
  .modal-nav {
    width: 50px;
    height: 50px;
    font-size: 1.2rem;
  }
  
  .prev-modal {
    left: 10px;
  }
  
  .next-modal {
    right: 10px;
  }
  
  .modal-close {
    top: 10px;
    right: 10px;
    width: 35px;
    height: 35px;
    font-size: 1rem;
  }
}
</style>
