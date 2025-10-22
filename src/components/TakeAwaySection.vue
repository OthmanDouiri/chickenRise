<template>
  <section id="takeaway" class="takeaway-section">
    <div class="container">
      <div class="row align-items-center">
        <!-- Columna Izquierda - Imagen -->
        <div class="col-lg-6">
          <div class="takeaway-image-container">
            <div class="image-wrapper">
              <img 
                src="/glovo.png" 
                alt="Chicken Rise Delivery" 
                class="takeaway-image"
              >
              <div class="image-overlay">
                <div class="overlay-content">
                  <i class="fas fa-motorcycle delivery-icon"></i>
                  <span class="overlay-text">Delivery disponible</span>
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
        
        <!-- Columna Derecha - Contenido -->
        <div class="col-lg-6">
          <div class="takeaway-content">
            <h2 class="takeaway-title">CHICKEN RISE<br><span class="highlight-text">DELIVERY</span></h2>
            
            <div class="takeaway-text">
              <p class="intro-text">
                Ahora y siempre, disfruta con quién quieras, dónde quieras
              </p>
              
              <p class="description-text">
                El auténtico sabor de Chicken Rise ahora llega hasta tu puerta. 
                Nuestros platos preparados con la misma dedicación y calidad de siempre, 
                listos para disfrutar en la comodidad de tu hogar.
              </p>
              
              
              <div class="cta-container">
                <a href="https://glovoapp.com" target="_blank" class="btn btn-glovo">
                  <i class="fas fa-motorcycle me-2"></i>
                  Pide en GLOVO
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'

onMounted(() => {
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
  const takeawayContent = document.querySelector('.takeaway-content')
  const takeawayImage = document.querySelector('.takeaway-image-container')
  
  if (takeawayContent) observer.observe(takeawayContent)
  if (takeawayImage) observer.observe(takeawayImage)
})
</script>

<style scoped>
.takeaway-section {
  background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 50%, #ffffff 100%);
  padding: 6rem 0;
  position: relative;
  overflow: hidden;
}

.takeaway-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle at 20% 80%, rgba(255, 193, 7, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(220, 53, 69, 0.1) 0%, transparent 50%),
    linear-gradient(45deg, transparent 48%, rgba(0, 0, 0, 0.02) 49%, rgba(0, 0, 0, 0.02) 51%, transparent 52%);
  pointer-events: none;
}

.container {
  position: relative;
  z-index: 2;
}

/* Columna Izquierda - Imagen */
.takeaway-image-container {
  position: relative;
  padding: 2rem;
  opacity: 0;
  transform: translateX(-50px);
  transition: all 0.8s ease;
}

.takeaway-image-container.animate-in {
  opacity: 1;
  transform: translateX(0);
}

.image-wrapper {
  position: relative;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.15),
    0 0 0 8px rgba(220, 53, 69, 0.1);
  transform: perspective(1000px) rotateY(5deg);
  transition: transform 0.5s ease;
}

.image-wrapper:hover {
  transform: perspective(1000px) rotateY(0deg) scale(1.02);
}

.takeaway-image {
  width: 100%;
  height: 500px;
  object-fit: cover;
  display: block;
  filter: brightness(0.9) contrast(1.1) saturate(1.1);
  transition: filter 0.3s ease;
}

.image-wrapper:hover .takeaway-image {
  filter: brightness(1) contrast(1.2) saturate(1.2);
}

.image-overlay {
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

.image-wrapper:hover .image-overlay {
  opacity: 1;
}

.overlay-content {
  text-align: center;
  color: white;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.image-wrapper:hover .overlay-content {
  transform: translateY(0);
}

.delivery-icon {
  font-size: 3rem;
  margin-bottom: 0.5rem;
  display: block;
  color: rgba(255, 255, 255, 0.9);
}

.overlay-text {
  font-size: 1.1rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Columna Derecha - Contenido */
.takeaway-content {
  padding: 2rem;
  opacity: 0;
  transform: translateX(50px);
  transition: all 0.8s ease 0.3s;
}

.takeaway-content.animate-in {
  opacity: 1;
  transform: translateX(0);
}

.takeaway-title {
  font-family: 'Inter', sans-serif;
  font-size: clamp(2.5rem, 4vw, 3.5rem);
  font-weight: 900;
  color: #333;
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

.takeaway-title::after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 0;
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #ffc107, #dc3545);
  border-radius: 2px;
}

.takeaway-text {
  color: #495057;
  line-height: 1.8;
  font-size: 1.1rem;
}

.intro-text {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 2rem;
  font-weight: 600;
  line-height: 1.4;
  font-style: italic;
}

.description-text {
  margin-bottom: 2rem;
  color: #6c757d;
  font-weight: 400;
  line-height: 1.7;
}

.delivery-features {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2.5rem;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  color: #495057;
  font-weight: 500;
  font-size: 1rem;
  padding: 0.75rem 0;
}

.feature-item i {
  color: #ffc107;
  font-size: 1.2rem;
  width: 24px;
  text-align: center;
}

.cta-container {
  margin-top: 2rem;
}

.btn-glovo {
  background: linear-gradient(45deg, #ffc107, #ffb300);
  color: #000;
  border: none;
  padding: 1rem 2.5rem;
  font-size: 1.2rem;
  font-weight: 700;
  font-family: 'Inter', sans-serif;
  border-radius: 50px;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(255, 193, 7, 0.3);
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-glovo:hover {
  background: linear-gradient(45deg, #ffb300, #ff8f00);
  color: #000;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255, 193, 7, 0.4);
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
  left: 20px;
  animation-delay: 0s;
}

.element-2 {
  width: 40px;
  height: 40px;
  bottom: 30px;
  right: -10px;
  animation-delay: 2s;
}

.element-3 {
  width: 80px;
  height: 80px;
  top: 50%;
  left: -30px;
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
  .takeaway-section {
    padding: 4rem 0;
  }
  
  .takeaway-content,
  .takeaway-image-container {
    padding: 1.5rem;
    text-align: center;
  }
  
  .takeaway-title {
    margin-bottom: 2rem;
  }
  
  .takeaway-title::after {
    left: 50%;
    transform: translateX(-50%);
  }
  
  .image-wrapper {
    transform: none;
    margin-top: 2rem;
  }
  
  .delivery-features {
    justify-content: center;
    align-items: center;
  }
}

@media (max-width: 768px) {
  .takeaway-section {
    padding: 3rem 0;
  }
  
  .takeaway-content,
  .takeaway-image-container {
    padding: 1rem;
  }
  
  .takeaway-title {
    font-size: 2rem;
    letter-spacing: 2px;
  }
  
  .takeaway-text {
    font-size: 1rem;
  }
  
  .intro-text {
    font-size: 1.2rem;
  }
  
  .takeaway-image {
    height: 300px;
  }
  
  .feature-item {
    font-size: 0.95rem;
  }
  
  .btn-glovo {
    padding: 0.8rem 2rem;
    font-size: 1.1rem;
  }
}

@media (max-width: 576px) {
  .takeaway-section {
    padding: 2rem 0;
  }
  
  .takeaway-title {
    font-size: 1.8rem;
    letter-spacing: 1px;
    margin-bottom: 1.5rem;
  }
  
  .intro-text {
    font-size: 1.1rem;
  }
  
  .takeaway-image {
    height: 250px;
  }
  
  .feature-item {
    font-size: 0.9rem;
    gap: 0.75rem;
  }
  
  .btn-glovo {
    padding: 0.75rem 1.8rem;
    font-size: 1rem;
  }
  
  .decorative-elements {
    display: none;
  }
}
</style>
