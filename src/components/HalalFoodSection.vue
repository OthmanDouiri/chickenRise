<template>
  <section id="halal" class="halal-section py-5">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-lg-6 order-lg-1 order-2">
          <div class="halal-content">
            <h2 class="section-title mb-4">
              <i class="fas fa-shield-alt text-success me-3"></i>
              Halal Food
            </h2>
            <p class="section-description mb-4">
              En Chicken Rise, nos comprometemos a ofrecer comida 100% halal certificada. 
              Todos nuestros ingredientes y procesos de preparación siguen estrictamente 
              los estándares halal para garantizar que puedas disfrutar de nuestros platos 
              con total tranquilidad.
            </p>
            
            <div class="halal-features">
              <div class="feature-item mb-3">
                <i class="fas fa-check-circle text-success me-3"></i>
                <span>Carne halal certificada</span>
              </div>
              <div class="feature-item mb-3">
                <i class="fas fa-check-circle text-success me-3"></i>
                <span>Procesos de preparación supervisados</span>
              </div>
              <div class="feature-item mb-3">
                <i class="fas fa-check-circle text-success me-3"></i>
                <span>Ingredientes verificados y aprobados</span>
              </div>
              <div class="feature-item mb-3">
                <i class="fas fa-check-circle text-success me-3"></i>
                <span>Cocina dedicada sin contaminación cruzada</span>
              </div>
            </div>

            <div class="certification-badge mt-4">
              <div class="badge-container">
                <i class="fas fa-award text-warning"></i>
                <div class="badge-text">
                  <strong>Certificación Halal</strong>
                  <br>
                  <small>Verificado por autoridades religiosas</small>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="col-lg-6 order-lg-2 order-1 mb-lg-0 mb-4">
          <div class="halal-visual">
            <div class="halal-image-grid">
              <div class="image-card main-image">
                <div class="image-placeholder">
                  <i class="fas fa-certificate"></i>
                  <span>Certificación Halal</span>
                </div>
              </div>
              <div class="image-card secondary-image">
                <div class="image-placeholder">
                  <i class="fas fa-shield-alt"></i>
                  <span>Proceso Verificado</span>
                </div>
              </div>
              <div class="image-card secondary-image">
                <div class="image-placeholder">
                  <i class="fas fa-award"></i>
                  <span>Calidad Garantizada</span>
                </div>
              </div>
            </div>
            
            <div class="floating-elements">
              <div class="floating-icon halal-icon-1">
                <i class="fas fa-heart text-danger"></i>
              </div>
              <div class="floating-icon halal-icon-2">
                <i class="fas fa-star text-warning"></i>
              </div>
              <div class="floating-icon halal-icon-3">
                <i class="fas fa-check-circle text-success"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div class="row mt-5">
        <div class="col-12">
          <div class="halal-commitment bg-white p-4 rounded-4 shadow-sm">
            <div class="row align-items-center">
              <div class="col-md-8">
                <h4 class="mb-2">
                  <i class="fas fa-mosque text-success me-2"></i>
                  Nuestro Compromiso con la Comunidad
                </h4>
                <p class="mb-0 text-muted">
                  Entendemos la importancia de mantener los valores religiosos y alimentarios. 
                  Por eso, trabajamos continuamente para asegurar que cada plato cumpla con 
                  los más altos estándares halal.
                </p>
              </div>
              <div class="col-md-4 text-md-end text-center mt-md-0 mt-3">
                <a href="#contact" class="btn btn-success btn-lg smooth-scroll">
                  <i class="fas fa-phone-alt me-2"></i>
                  Consultar
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
  // Add smooth scroll functionality
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
})
</script>

<style scoped>
.halal-section {
  background: linear-gradient(135deg, #fff 0%, #f8f9fa 100%);
  min-height: 100vh;
  position: relative;
  overflow: hidden;
}

.halal-section::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -50%;
  width: 100%;
  height: 200%;
  background: radial-gradient(circle, rgba(40, 167, 69, 0.05) 0%, transparent 70%);
  z-index: 1;
}

.container {
  position: relative;
  z-index: 2;
}

.section-title {
  font-family: 'Playfair Display', serif;
  font-size: 2.5rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 1.5rem;
}

.section-description {
  font-size: 1.1rem;
  color: #666;
  line-height: 1.7;
}

.halal-features {
  margin: 2rem 0;
}

.feature-item {
  font-size: 1.1rem;
  color: #333;
  font-weight: 500;
  display: flex;
  align-items: center;
}

.feature-item i {
  font-size: 1.2rem;
}

.certification-badge {
  background: linear-gradient(135deg, #fff 0%, #f8f9fa 100%);
  border: 2px solid #28a745;
  border-radius: 15px;
  padding: 1.5rem;
  box-shadow: 0 5px 15px rgba(40, 167, 69, 0.1);
}

.badge-container {
  display: flex;
  align-items: center;
}

.badge-container i {
  font-size: 3rem;
  margin-right: 1rem;
}

.badge-text {
  color: #333;
}

.halal-visual {
  position: relative;
  height: 400px;
}

.halal-image-grid {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 15px;
  height: 100%;
}

.main-image {
  grid-row: 1 / 3;
}

.image-card {
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.image-card:hover {
  transform: scale(1.05);
}

.image-placeholder {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #28a745, #20c997);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 2rem;
  text-align: center;
  font-weight: 600;
}

.secondary-image .image-placeholder {
  font-size: 1.5rem;
}

.image-placeholder span {
  font-size: 0.9rem;
  margin-top: 10px;
}

.secondary-image .image-placeholder span {
  font-size: 0.8rem;
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
}

.floating-icon {
  position: absolute;
  font-size: 1.5rem;
  opacity: 0.7;
  animation: float 3s ease-in-out infinite;
}

.halal-icon-1 {
  top: 10%;
  right: 20%;
  animation-delay: 0s;
}

.halal-icon-2 {
  top: 60%;
  right: 5%;
  animation-delay: 1s;
}

.halal-icon-3 {
  top: 80%;
  left: 10%;
  animation-delay: 2s;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

.halal-commitment {
  border-left: 4px solid #28a745;
}

.btn-success {
  background: linear-gradient(45deg, #28a745, #20c997);
  border: none;
  border-radius: 25px;
  padding: 12px 25px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-success:hover {
  background: linear-gradient(45deg, #20c997, #28a745);
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(40, 167, 69, 0.3);
}

/* Responsive Design */
@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }
  
  .halal-visual {
    height: 300px;
  }
  
  .image-placeholder {
    font-size: 1.5rem;
  }
  
  .secondary-image .image-placeholder {
    font-size: 1rem;
  }
  
  .floating-icon {
    font-size: 1rem;
  }
  
  .badge-container {
    flex-direction: column;
    text-align: center;
  }
  
  .badge-container i {
    margin-right: 0;
    margin-bottom: 1rem;
  }
}
</style>
