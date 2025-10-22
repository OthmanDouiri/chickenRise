<template>
  <section id="location" class="location-section">
    <div class="container">
      <div class="row align-items-center">
        <!-- Columna Izquierda - Contenido -->
        <div class="col-lg-6">
          <div class="location-content">
            <h2 class="location-title">NUESTRA<br><span class="highlight-text">UBICACIÓN</span></h2>
            
            <div class="location-text">
              <p class="intro-text">
                Te esperamos en el corazón de Granada
              </p>
              
              <div class="address-info">
                <div class="info-item">
                  <i class="fas fa-map-marker-alt"></i>
                  <div class="info-details">
                    <h5>Dirección</h5>
                    <p>Calle Almenillas N10 Local 3<br>Granada, España</p>
                  </div>
                </div>
                
                <div class="info-item">
                  <i class="fas fa-clock"></i>
                  <div class="info-details">
                    <h5>Horarios</h5>
                    <p>Lunes - Domingo<br><strong>12:30 - 00:00</strong></p>
                    <span class="status-badge" :class="{ 'open': isOpen, 'closed': !isOpen }">
                      <i class="fas fa-circle"></i>
                      {{ isOpen ? 'Abierto ahora' : 'Cerrado' }}
                    </span>
                  </div>
                </div>
                
                <div class="info-item">
                  <i class="fas fa-phone"></i>
                  <div class="info-details">
                    <h5>Teléfono</h5>
                    <p><a href="tel:604901903" class="phone-link">604 901 903</a></p>
                  </div>
                </div>
              </div>
              
              <div class="cta-container">
                <a href="https://maps.app.goo.gl/AQRZkgkTyTfEGt2R6?g_st=iw" target="_blank" class="btn btn-location">
                  <i class="fas fa-map me-2"></i>
                  Ver en Google Maps
                </a>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Columna Derecha - Mapa -->
        <div class="col-lg-6">
          <div class="location-image-container">
            <div class="map-wrapper">
              <a href="https://maps.app.goo.gl/AQRZkgkTyTfEGt2R6?g_st=iw" target="_blank" rel="noopener noreferrer" class="map-link">
                <iframe 
                  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3179.0234567890123!2d-3.5996!3d37.1777!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd71fc68c8a9f5ab%3A0x123456789abcdef!2sCalle%20Almenillas%2C%2010%2C%20Local%203%2C%2018002%20Granada%2C%20Spain!5e0!3m2!1sen!2ses!4v1697985600000!5m2!1sen!2ses"
                  width="100%" 
                  height="300" 
                  style="border:0; border-radius: 20px;" 
                  allowfullscreen="" 
                  loading="lazy" 
                  referrerpolicy="no-referrer-when-downgrade"
                  class="embedded-google-map">
                </iframe>
                <div class="map-overlay">
                  <div class="overlay-content">
                    <i class="fas fa-directions map-icon"></i>
                    <span class="overlay-text">Cómo llegar</span>
                  </div>
                </div>
              </a>
            </div>
            
            <!-- Características del local -->
            <div class="location-features">
              <div class="feature-grid">
                <div class="feature-item">
                  <i class="fas fa-car"></i>
                  <span>Parking</span>
                </div>
                <div class="feature-item">
                  <i class="fas fa-wifi"></i>
                  <span>WiFi Gratis</span>
                </div>
                <div class="feature-item">
                  <i class="fas fa-credit-card"></i>
                  <span>Tarjetas</span>
                </div>
                <div class="feature-item">
                  <i class="fas fa-motorcycle"></i>
                  <span>Delivery</span>
                </div>
              </div>
            </div>
            
            <!-- Elementos decorativos -->
            <div class="decorative-elements">
              <div class="element element-1"></div>
              <div class="element element-2"></div>
              <div class="element element-3"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const isOpen = ref(true)

onMounted(() => {
  // Check if restaurant is currently open
  const now = new Date()
  const hour = now.getHours()
  const minute = now.getMinutes()
  const currentTime = hour + minute / 60
  
  // Restaurant hours: 12:30 - 00:00 (12.5 - 24.0)
  isOpen.value = currentTime >= 12.5 || currentTime < 1.0

  // Animación de entrada para el contenido
  const observerOptions = {
    threshold: 0.3,
    rootMargin: '0px 0px -50px 0px'
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
      }
    })
  }, observerOptions)

  // Observar elementos para animación
  const locationContent = document.querySelector('.location-content')
  const locationImage = document.querySelector('.location-image-container')
  
  if (locationContent) observer.observe(locationContent)
  if (locationImage) observer.observe(locationImage)
})
</script>

<style scoped>
.location-section {
  background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 50%, #1a1a1a 100%);
  padding: 6rem 0;
  position: relative;
  overflow: hidden;
}

.location-section::before {
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

/* Columna Izquierda - Contenido */
.location-content {
  padding: 2rem;
  opacity: 0;
  transform: translateX(-50px);
  transition: all 0.8s ease;
}

.location-content.animate-in {
  opacity: 1;
  transform: translateX(0);
}

.location-title {
  font-family: 'Inter', sans-serif;
  font-size: clamp(2.5rem, 4vw, 3.5rem);
  font-weight: 900;
  color: #f8f9fa;
  text-transform: uppercase;
  letter-spacing: 3px;
  margin-bottom: 2.5rem;
  position: relative;
  line-height: 1.1;
}

.highlight-text {
  color: #dc3545;
  display: block;
  font-weight: 900;
  margin-top: 0.5rem;
}

.location-title::after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 0;
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #dc3545, #ffc107);
  border-radius: 2px;
}

.location-text {
  color: #e9ecef;
  line-height: 1.8;
  font-size: 1.1rem;
}

.intro-text {
  font-size: 1.5rem;
  color: #f8f9fa;
  margin-bottom: 2.5rem;
  font-weight: 600;
  line-height: 1.4;
  font-style: italic;
}

.address-info {
  margin-bottom: 2.5rem;
}

.info-item {
  display: flex;
  align-items: flex-start;
  gap: 1.5rem;
  margin-bottom: 2rem;
  padding: 1.5rem 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.info-item:last-child {
  border-bottom: none;
}

.info-item i {
  color: #ffc107;
  font-size: 1.5rem;
  width: 24px;
  text-align: center;
  margin-top: 0.25rem;
}

.info-details h5 {
  color: #f8f9fa;
  font-weight: 600;
  margin-bottom: 0.5rem;
  font-size: 1.1rem;
}

.info-details p {
  color: #ced4da;
  margin-bottom: 0.5rem;
  line-height: 1.6;
}

.phone-link {
  color: #ffc107;
  text-decoration: none;
  font-weight: 600;
  font-size: 1.1rem;
}

.phone-link:hover {
  color: #fff;
}

.status-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.status-badge.open {
  background: rgba(40, 167, 69, 0.2);
  color: #28a745;
  border: 1px solid rgba(40, 167, 69, 0.3);
}

.status-badge.closed {
  background: rgba(220, 53, 69, 0.2);
  color: #dc3545;
  border: 1px solid rgba(220, 53, 69, 0.3);
}

.status-badge i {
  font-size: 0.7rem;
}

.cta-container {
  margin-top: 2rem;
}

.btn-location {
  background: linear-gradient(45deg, #dc3545, #c82333);
  color: #fff;
  border: none;
  padding: 1rem 2.5rem;
  font-size: 1.1rem;
  font-weight: 700;
  font-family: 'Inter', sans-serif;
  border-radius: 50px;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(220, 53, 69, 0.3);
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-location:hover {
  background: linear-gradient(45deg, #c82333, #a71e2a);
  color: #fff;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(220, 53, 69, 0.4);
}

/* Columna Derecha - Mapa */
.location-image-container {
  position: relative;
  padding: 2rem;
  opacity: 0;
  transform: translateX(50px);
  transition: all 0.8s ease 0.3s;
}

.location-image-container.animate-in {
  opacity: 1;
  transform: translateX(0);
}

.map-wrapper {
  position: relative;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.4),
    0 0 0 8px rgba(255, 193, 7, 0.1);
  transform: perspective(1000px) rotateY(-5deg);
  transition: transform 0.5s ease;
}

.map-wrapper:hover {
  transform: perspective(1000px) rotateY(0deg) scale(1.02);
}

.map-link {
  display: block;
  width: 100%;
  height: 100%;
  text-decoration: none;
  position: relative;
}

.embedded-google-map {
  filter: brightness(0.9) contrast(1.1) saturate(0.9);
  transition: filter 0.3s ease;
  pointer-events: none;
}

.map-wrapper:hover .embedded-google-map {
  filter: brightness(1) contrast(1.2) saturate(1.1);
}

.map-placeholder {
  width: 100%;
  height: 300px;
  background: linear-gradient(135deg, #dc3545, #c82333);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  text-align: center;
  position: relative;
}

.map-placeholder i {
  font-size: 4rem;
  margin-bottom: 1rem;
  opacity: 0.9;
}

.map-placeholder h5 {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.map-placeholder p {
  font-size: 1rem;
  opacity: 0.9;
  margin: 0;
}

.map-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg, 
    rgba(255, 193, 7, 0.8) 0%, 
    rgba(0, 0, 0, 0.3) 50%, 
    rgba(220, 53, 69, 0.6) 100%
  );
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.map-wrapper:hover .map-overlay {
  opacity: 1;
}

.overlay-content {
  text-align: center;
  color: white;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.map-wrapper:hover .overlay-content {
  transform: translateY(0);
}

.map-icon {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  display: block;
}

.overlay-text {
  font-size: 1.1rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.location-features {
  margin-top: 2rem;
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.feature-item {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
}

.feature-item:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateY(-2px);
}

.feature-item i {
  color: #ffc107;
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
  display: block;
}

.feature-item span {
  color: #f8f9fa;
  font-size: 0.9rem;
  font-weight: 500;
}

/* Elementos Decorativos */
.decorative-elements {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
}

.element {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(45deg, rgba(255, 193, 7, 0.2), rgba(220, 53, 69, 0.2));
  animation: float 6s ease-in-out infinite;
}

.element-1 {
  width: 60px;
  height: 60px;
  top: -20px;
  right: 20px;
  animation-delay: 0s;
}

.element-2 {
  width: 40px;
  height: 40px;
  bottom: 30px;
  left: -10px;
  animation-delay: 2s;
}

.element-3 {
  width: 80px;
  height: 80px;
  top: 50%;
  right: -30px;
  animation-delay: 4s;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
    opacity: 0.6;
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
    opacity: 1;
  }
}

/* Responsive Design */
@media (max-width: 991.98px) {
  .location-section {
    padding: 4rem 0;
  }
  
  .location-content,
  .location-image-container {
    padding: 1.5rem;
    text-align: center;
  }
  
  .location-title {
    margin-bottom: 2rem;
  }
  
  .location-title::after {
    left: 50%;
    transform: translateX(-50%);
  }
  
  .map-wrapper {
    transform: none;
    margin-top: 2rem;
  }
  
  .info-item {
    justify-content: center;
    text-align: center;
  }
}

@media (max-width: 768px) {
  .location-section {
    padding: 3rem 0;
  }
  
  .location-content,
  .location-image-container {
    padding: 1rem;
  }
  
  .location-title {
    font-size: 2rem;
    letter-spacing: 2px;
  }
  
  .location-text {
    font-size: 1rem;
  }
  
  .intro-text {
    font-size: 1.2rem;
  }
  
  .map-placeholder {
    height: 300px;
  }
  
  .feature-grid {
    grid-template-columns: 1fr;
  }
  
  .btn-location {
    padding: 0.8rem 2rem;
    font-size: 1rem;
  }
}

@media (max-width: 576px) {
  .location-section {
    padding: 2rem 0;
  }
  
  .location-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
    margin-bottom: 1.5rem;
  }
  
  .intro-text {
    font-size: 1.1rem;
  }
  
  .map-placeholder {
    height: 250px;
  }
  
  .map-placeholder i {
    font-size: 3rem;
  }
  
  .info-item {
    padding: 1rem 0;
    gap: 1rem;
  }
  
  .btn-location {
    padding: 0.75rem 1.8rem;
    font-size: 0.95rem;
  }
  
  .decorative-elements {
    display: none;
  }
}
</style>
