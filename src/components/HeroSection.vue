<template>
  <section id="home" class="hero-section">
    <!-- Hero Background with Image -->
    <div class="hero-bg" style="background-image: url('/hero-bg.png')">
      

      <div class="container h-100">
        <div class="row h-100">
          <!-- Left Content Panel -->
          <div class="col-lg-6 d-flex align-items-center">
            <div class="hero-content">
              <h1 class="hero-headline animate__animated animate__fadeInUp">
                EL MEJOR POLLO<br>
                <span class="highlight-text">para compartir con amigos</span>
              </h1>
              
              <div class="hero-cta animate__animated animate__fadeInUp animate__delay-1s">
                <a href="#takeaway" class="btn btn-coupon smooth-scroll pulse-button">
                <i class="fas fa-utensils me-2" aria-hidden="true"></i>
                 Ver Menú
                </a>
              </div>
            </div>
          </div>

         
        </div>
      </div>

      <!-- Bottom Banner -->
      <div class="hero-bottom-banner" ref="bannerContainer">
        <div class="banner-scroll-container" ref="scrollContainer">
          <div class="banner-content" ref="bannerContent">
            <span class="banner-text">{{ bannerText }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Banner text - single string with all content
const bannerText = ref('🚀 Entrega más rápida ⭐ ✅ Calidad Garantizada ⭐ 🥗 100% Halal ⭐ 🔥 Pollo Fresco ⭐ ⭐ 5 Estrellas ⭐ 🎯 Mejor Precio ⭐ 📞 Pedidos: 604 901 903 ⭐ 🏆 Mejor de Granada ⭐ 🕐 Abierto hasta 00:00 ⭐ 💯 Satisfacción Garantizada ⭐ ')

// Refs for DOM elements
const bannerContainer = ref(null)
const scrollContainer = ref(null)
const bannerContent = ref(null)

// Animation variables
let animationId = null
let scrollPosition = 0
let speed = 1
let containerWidth = 0
let contentWidth = 0

// Initialize infinite scroll
const initInfiniteScroll = () => {
  if (!bannerContainer.value || !bannerContent.value) return
  
  // Get container and content widths
  containerWidth = bannerContainer.value.offsetWidth
  contentWidth = bannerContent.value.scrollWidth
  
  // Duplicate content for seamless loop
  const originalContent = bannerContent.value.innerHTML
  bannerContent.value.innerHTML = originalContent + originalContent
  
  // Update content width after duplication
  contentWidth = bannerContent.value.scrollWidth / 2
  
  // Set responsive speed based on screen size
  updateSpeed()
  
  // Start animation
  animate()
}

// Update speed based on screen size
const updateSpeed = () => {
  const width = window.innerWidth
  if (width < 576) {
    speed = 2.5 // Slower on mobile
  } else if (width < 768) {
    speed = 2.7 // Medium on tablet
  } else if (width < 992) {
    speed = 3.9 // Faster on laptop
  } else {
    speed = 4.2 // Fastest on desktop
  }
}

// Animation loop
const animate = () => {
  if (!bannerContent.value) return
  
  scrollPosition -= speed
  
  // Reset position for infinite loop
  if (Math.abs(scrollPosition) >= contentWidth) {
    scrollPosition = 0
  }
  
  // Apply transform
  bannerContent.value.style.transform = `translateX(${scrollPosition}px)`
  
  // Continue animation
  animationId = requestAnimationFrame(animate)
}

// Handle resize
const handleResize = () => {
  if (bannerContainer.value && bannerContent.value) {
    containerWidth = bannerContainer.value.offsetWidth
    contentWidth = bannerContent.value.scrollWidth / 2
    updateSpeed()
  }
}

// Pause animation on hover
const pauseAnimation = () => {
  if (animationId) {
    cancelAnimationFrame(animationId)
    animationId = null
  }
}

// Resume animation
const resumeAnimation = () => {
  if (!animationId) {
    animate()
  }
}

onMounted(() => {
  // Add smooth scroll functionality for hero buttons
  const scrollLinks = document.querySelectorAll('.smooth-scroll')
  scrollLinks.forEach(link => {
    link.addEventListener('click', (e) => {
      e.preventDefault()
      const targetId = link.getAttribute('href')
      const targetElement = document.querySelector(targetId)
      if (targetElement) {
        const offsetTop = targetElement.offsetTop - 80
        window.scrollTo({
          top: offsetTop,
          behavior: 'smooth'
        })
      }
    })
  })
  
  // Initialize banner scroll after a short delay
  setTimeout(() => {
    initInfiniteScroll()
  }, 100)
  
  // Add event listeners
  window.addEventListener('resize', handleResize)
  
  // Pause/resume on hover
  if (bannerContainer.value) {
    bannerContainer.value.addEventListener('mouseenter', pauseAnimation)
    bannerContainer.value.addEventListener('mouseleave', resumeAnimation)
  }
})

onUnmounted(() => {
  // Clean up
  if (animationId) {
    cancelAnimationFrame(animationId)
  }
  window.removeEventListener('resize', handleResize)
  
  if (bannerContainer.value) {
    bannerContainer.value.removeEventListener('mouseenter', pauseAnimation)
    bannerContainer.value.removeEventListener('mouseleave', resumeAnimation)
  }
})
</script>

<style scoped>
.hero-section {
  height: 100vh;
  position: relative;
  overflow: hidden;
}

.hero-bg {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #e85d75 0%, #dc3545 40%, #c82333 100%);
  background-size: cover;
  background-position: center;
  background-blend-mode: multiply;
  position: relative;
  display: flex;
  flex-direction: column;
}



.wavy-line::before {
  content: '';
  position: absolute;
  top: -15px;
  left: 20%;
  width: 40%;
  height: 6px;
  background: #fff;
  border-radius: 10px;
  transform: rotate(15deg);
}

.wavy-line::after {
  content: '';
  position: absolute;
  top: 15px;
  left: 30%;
  width: 30%;
  height: 6px;
  background: #fff;
  border-radius: 10px;
  transform: rotate(-10deg);
}

/* Logo in Corner */
.hero-logo-corner {
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 10;
}

.corner-logo {
  height: 50px;
  width: auto;
  filter: brightness(1.2);
}

/* Hero Content */
.hero-content {
  padding: 2rem;
  z-index: 3;
  max-width: 100%;
  width: 100%;
}

.hero-headline {
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  font-weight: 800;
  color: #df0e0e;
  line-height: 1.1;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  margin-bottom: 2rem;
  font-family:Georgia, 'Times New Roman', Times, serif;
  word-wrap: break-word;
  hyphens: auto;
}

.highlight-text {
  color: #fff;
  display: block;
  font-weight: 900;
  margin-top: 0.5rem;
}

/* CTA Button */
.btn-coupon {
  background: #e0241f;
  color: #fff;
  border: none;
  padding: clamp(12px, 2vw, 18px) clamp(25px, 4vw, 35px);
  font-size: clamp(1rem, 2vw, 1.2rem);
  font-weight: 700;
  font-family: 'Inter', sans-serif;
  border-radius: 8px;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  width: auto;
  min-width: 200px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-coupon:hover {
  background: #1a1a1a;
  color: #fff;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
}

/* Food Container */
.hero-food-container {
  position: relative;
  width: 100%;
  height: 400px;
}

.food-image-wrapper {
  width: 100%;
  height: 100%;
  border-radius: 20px;
  overflow: hidden;
  position: relative;
}

.food-placeholder {
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, #8B4513, #A0522D);
  background-image: 
    radial-gradient(circle at 30% 70%, #FFD700 20px, transparent 20px),
    radial-gradient(circle at 60% 40%, #FFA500 15px, transparent 15px),
    radial-gradient(circle at 80% 80%, #FF6347 25px, transparent 25px);
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid rgba(255, 255, 255, 0.2);
}

.food-description {
  text-align: center;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8);
}

.food-description h3 {
  font-size: 1.8rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.food-description p {
  font-size: 1rem;
  opacity: 0.9;
}

/* Steam Effect */
.steam-effect {
  position: absolute;
  top: 10px;
  right: 20px;
}

.steam {
  width: 3px;
  height: 30px;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 50px;
  position: absolute;
  animation: steam-rise 2s infinite ease-in-out;
}

.steam-1 {
  left: 0;
  animation-delay: 0s;
}

.steam-2 {
  left: 8px;
  animation-delay: 0.5s;
}

.steam-3 {
  left: 16px;
  animation-delay: 1s;
}

@keyframes steam-rise {
  0% {
    opacity: 0;
    transform: translateY(20px) scale(1);
  }
  50% {
    opacity: 1;
    transform: translateY(-10px) scale(1.2);
  }
  100% {
    opacity: 0;
    transform: translateY(-40px) scale(0.8);
  }
}

/* Halal Badge */
.halal-badge {
  position: absolute;
  top: -10px;
  right: -10px;
  z-index: 5;
}

.badge-circle {
  width: 100px;
  height: 100px;
  background: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  border: 3px solid #28a745;
  transform: rotate(-15deg);
}

.badge-text {
  text-align: center;
  color: #28a745;
  font-weight: 900;
  font-size: 0.7rem;
  line-height: 1.1;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Bottom Banner */
.hero-bottom-banner {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(90deg, #000000, #1a1a1a, #000000);
  padding: 1rem 0;
  z-index: 4;
  overflow: hidden;
  border-top: 2px solid #ffc107;
}

.banner-scroll-container {
  width: 100%;
  overflow: hidden;
}

.banner-content {
  display: inline-block;
  white-space: nowrap;
  will-change: transform;
  transition: none;
}

.banner-text {
  color: #fff;
  font-weight: 700;
  font-size: 1.1rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.8);
  display: inline-block;
  padding: 0 2rem;
}

@keyframes twinkle {
  0% {
    opacity: 0.8;
    transform: scale(1);
  }
  100% {
    opacity: 1;
    transform: scale(1.2);
  }
}

/* Responsive Banner Adjustments */
@media (max-width: 768px) {
  .banner-text {
    font-size: 0.9rem;
    letter-spacing: 1.5px;
    padding: 0 1.5rem;
  }
}

@media (max-width: 576px) {
  .hero-bottom-banner {
    padding: 0.8rem 0;
  }
  
  .banner-text {
    font-size: 0.8rem;
    letter-spacing: 1px;
    padding: 0 1rem;
  }
}

@media (max-width: 480px) {
  .banner-text {
    font-size: 0.75rem;
    letter-spacing: 0.5px;
  }
}

/* Pulse Animation for CTA */
.pulse-button {
  animation: pulse-coupon 2s infinite;
}

@keyframes pulse-coupon {
  0% {
    box-shadow: 0 0 0 0 rgba(44, 44, 44, 0.7);
  }
  70% {
    box-shadow: 0 0 0 10px rgba(44, 44, 44, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(44, 44, 44, 0);
  }
}

/* Responsive Design */
@media (max-width: 1200px) {
  .hero-content {
    padding: 1.5rem;
  }
}

@media (max-width: 991.98px) {
  .hero-content {
    padding: 1.5rem 1rem;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 50vh;
  }
  
  .hero-headline {
    text-align: center;
    margin-bottom: 1.5rem;
  }
  
  .hero-cta {
    width: 100%;
    display: flex;
    justify-content: center;
  }
  
  .btn-coupon {
    width: 80%;
    max-width: 300px;
  }
}

@media (max-width: 768px) {
  .hero-content {
    padding: 1rem;
    min-height: 40vh;
  }
  
  .hero-headline {
    margin-bottom: 1.25rem;
    line-height: 1.2;
  }
  
  .highlight-text {
    font-size: 0.9em;
    margin-top: 0.25rem;
  }
  
  .btn-coupon {
    width: 90%;
    max-width: 280px;
    min-width: 180px;
  }
}

@media (max-width: 576px) {
  .hero-section {
    height: 100vh;
    display: flex;
    flex-direction: column;
  }
  
  .hero-bg {
    flex: 1;
  }
  
  .hero-content {
    padding: 0.75rem;
    min-height: 35vh;
    justify-content: flex-start;
    padding-top: 2rem;
  }
  
  .hero-headline {
    margin-bottom: 1rem;
    line-height: 1.15;
    font-size: clamp(2.8rem, 8vw, 4rem);
  }
  
  .highlight-text {
    font-size: 2.1em;
    font-weight: 900;
    text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.7);
  }
  
  .btn-coupon {
    width: 95%;
    max-width: 250px;
    min-width: 160px;
    margin-top: 0.5rem;
  }
  
  .hero-cta {
    margin-top: 0.5rem;
  }
}

@media (max-width: 480px) {
  .hero-content {
    padding: 0.5rem;
    padding-top: 1.5rem;
  }
  
  .hero-headline {
    margin-bottom: 0.75rem;
    font-size: 3.8rem;
  }
  
  .highlight-text {
    font-size: 1.05em;
  }
  
  .btn-coupon {
    width: 100%;
    max-width: 220px;
    font-size: 0.9rem;
  }
}

@media (max-width: 360px) {
  .hero-content {
    padding: 0.25rem;
    padding-top: 1rem;
  }
  
  .hero-headline {
    font-size: clamp(2.2rem, 6vw, 3rem);
  }
  
  .highlight-text {
    font-size: 1em;
  }
  
  .btn-coupon {
    max-width: 200px;
    font-size: 0.85rem;
    min-width: 140px;
  }
}
</style>
