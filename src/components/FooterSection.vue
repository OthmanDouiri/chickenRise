<template>
  <footer id="contact" class="footer-section">
    <div class="container">
      <div class="row g-4">
        <!-- Restaurant Info -->
        <div class="col-lg-4 col-md-6">
          <div class="footer-content">
            <div class="footer-logo">
              <img src="/logo-bg.png" alt="Chicken Rise" class="footer-logo-img">
            </div>
            <p class="footer-slogan">Mucho más que pollo</p>
            <p class="footer-description">
              El mejor pollo halal de Granada. Comida de calidad, 
              sabor auténtico y servicio excepcional desde 2020.
            </p>
            <div class="certifications">
              <div class="cert-badge">
                <i class="fas fa-shield-alt text-success"></i>
                <span>Halal Certified</span>
              </div>
              <div class="cert-badge">
                <i class="fas fa-award text-warning"></i>
                <span>Quality Assured</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Contact Info -->
        <div class="col-lg-4 col-md-6">
          <div class="footer-content">
            <h5 class="footer-subtitle">
              <i class="fas fa-phone-alt me-2 text-danger"></i>
              Contacto
            </h5>
            <div class="contact-items">
              <div class="contact-item">
                <i class="fas fa-phone"></i>
                <div class="contact-details">
                  <a href="tel:604901903" class="contact-link">604 901 903</a>
                  <small>Lunes - Domingo: 12:30 - 00:00</small>
                </div>
              </div>
              
              <div class="contact-item">
                <i class="fas fa-map-marker-alt"></i>
                <div class="contact-details">
                  <span>Calle Almenillas N10 Local 3</span>
                  <small>Granada, España</small>
                </div>
              </div>
              
              <div class="contact-item">
                <i class="fas fa-envelope"></i>
                <div class="contact-details">
                  <a href="mailto:info@chickenrise.es" class="contact-link">info@chickenrise.es</a>
                  <small>Respuesta en 24h</small>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Social Media & Quick Links -->
        <div class="col-lg-4 col-md-12">
          <div class="footer-content">
            <h5 class="footer-subtitle">
              <i class="fas fa-share-alt me-2 text-info"></i>
              Síguenos
            </h5>
            <div class="social-links">
              <a href="#" class="social-link facebook" target="_blank" rel="noopener">
                <i class="fab fa-facebook-f"></i>
                <span>Facebook</span>
              </a>
              <a href="#" class="social-link instagram" target="_blank" rel="noopener">
                <i class="fab fa-instagram"></i>
                <span>Instagram</span>
              </a>
              <a href="#" class="social-link whatsapp" target="_blank" rel="noopener">
                <i class="fab fa-whatsapp"></i>
                <span>WhatsApp</span>
              </a>
              <a href="#" class="social-link tiktok" target="_blank" rel="noopener">
                <i class="fab fa-tiktok"></i>
                <span>TikTok</span>
              </a>
            </div>
            
            <div class="quick-links mt-4">
              <h6 class="quick-links-title">Enlaces Rápidos</h6>
              <div class="links-grid">
                <a href="#home" class="quick-link smooth-scroll">Inicio</a>
                <a href="#takeaway" class="quick-link smooth-scroll">Menú</a>
                <a href="#halal" class="quick-link smooth-scroll">Halal</a>
                <a href="#location" class="quick-link smooth-scroll">Ubicación</a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Footer Bottom -->
      <div class="footer-bottom">
        <div class="row align-items-center">
          <div class="col-md-6">
            <p class="copyright">
              © {{ currentYear }} Chicken Rise. Todos los derechos reservados.
            </p>
          </div>
          
        </div>
      </div>
    </div>

    <!-- Back to Top Button -->
    <button class="back-to-top" @click="scrollToTop" :class="{ 'visible': showBackToTop }">
      <i class="fas fa-chevron-up"></i>
    </button>
  </footer>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const currentYear = new Date().getFullYear()
const showBackToTop = ref(false)

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

const handleScroll = () => {
  showBackToTop.value = window.pageYOffset > 300
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
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

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.footer-section {
  background: linear-gradient(135deg, #000 0%, #1a1a1a 100%);
  color: #fff;
  padding: 4rem 0 2rem;
  position: relative;
  overflow: hidden;
}

.footer-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, #dc3545, #ffc107, #dc3545);
}

.footer-content {
  height: 100%;
}

.footer-logo {
  margin-bottom: 1rem;
  text-align: left;
}

.footer-logo-img {
  height: 120px;
  width: auto;
  transition: all 0.3s ease;
  filter: brightness(1.1) contrast(1.1);
  border-radius: 8px;
}

.footer-logo:hover .footer-logo-img {
  filter: brightness(1.3) contrast(1.2) drop-shadow(0 0 15px rgba(255, 193, 7, 0.4));
  transform: scale(1.05);
}

.footer-slogan {
  font-family: 'Dancing Script', cursive;
  color: #ffc107;
  font-size: 1.4rem;
  margin-bottom: 1rem;
}

.footer-description {
  color: #ccc;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.footer-subtitle {
  font-family: 'Playfair Display', serif;
  color: #fff;
  font-weight: 600;
  margin-bottom: 1.5rem;
  font-size: 1.2rem;
}

.certifications {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.cert-badge {
  display: flex;
  align-items: center;
  background: rgba(255, 255, 255, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  transition: background 0.3s ease;
}

.cert-badge:hover {
  background: rgba(255, 255, 255, 0.2);
}

.cert-badge i {
  margin-right: 0.5rem;
  font-size: 1rem;
}

.contact-items {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.contact-item i {
  color: #dc3545;
  font-size: 1.2rem;
  margin-top: 0.2rem;
  flex-shrink: 0;
}

.contact-details {
  display: flex;
  flex-direction: column;
}

.contact-link {
  color: #fff;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
}

.contact-link:hover {
  color: #ffc107;
}

.contact-details small {
  color: #ccc;
  font-size: 0.85rem;
}

.social-links {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  margin-bottom: 2rem;
}

.social-link {
  display: flex;
  align-items: center;
  padding: 0.75rem 1rem;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  text-decoration: none;
  color: #fff;
  transition: all 0.3s ease;
  font-weight: 500;
}

.social-link i {
  font-size: 1.2rem;
  margin-right: 0.5rem;
}

.social-link:hover {
  color: #fff;
  transform: translateY(-2px);
}

.social-link.facebook:hover {
  background: #1877f2;
  box-shadow: 0 5px 15px rgba(24, 119, 242, 0.3);
}

.social-link.instagram:hover {
  background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
  box-shadow: 0 5px 15px rgba(188, 24, 136, 0.3);
}

.social-link.whatsapp:hover {
  background: #25d366;
  box-shadow: 0 5px 15px rgba(37, 211, 102, 0.3);
}

.social-link.tiktok:hover {
  background: #000;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

.quick-links-title {
  color: #ffc107;
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 0.75rem;
}

.links-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.5rem;
}

.quick-link {
  color: #ccc;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.3s ease;
  padding: 0.25rem 0;
}

.quick-link:hover {
  color: #ffc107;
}

.newsletter-section {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.newsletter-title {
  color: #fff;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.newsletter-text {
  color: #ccc;
  margin-bottom: 0;
}

.newsletter-input {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.3);
  color: #fff;
  border-radius: 25px 0 0 25px;
}

.newsletter-input::placeholder {
  color: #ccc;
}

.newsletter-input:focus {
  background: rgba(255, 255, 255, 0.2);
  border-color: #ffc107;
  color: #fff;
  box-shadow: none;
}

.newsletter-btn {
  border-radius: 0 25px 25px 0;
  font-weight: 600;
  background: linear-gradient(45deg, #ffc107, #ffb300);
  border: none;
  color: #000;
}

.newsletter-btn:hover {
  background: linear-gradient(45deg, #ffb300, #ff8f00);
  color: #000;
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  margin-top: 3rem;
  padding-top: 2rem;
}

.copyright {
  color: #ccc;
  margin: 0;
  font-size: 0.9rem;
}

.footer-links {
  display: flex;
  justify-content: flex-end;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.footer-link {
  color: #ccc;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: #ffc107;
}

.back-to-top {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 50px;
  height: 50px;
  background: linear-gradient(45deg, #dc3545, #c82333);
  color: #fff;
  border: none;
  border-radius: 50%;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  opacity: 0;
  visibility: hidden;
  z-index: 1000;
  box-shadow: 0 4px 15px rgba(220, 53, 69, 0.3);
}

.back-to-top.visible {
  opacity: 1;
  visibility: visible;
}

.back-to-top:hover {
  background: linear-gradient(45deg, #c82333, #a71e2a);
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(220, 53, 69, 0.4);
}

/* Responsive Design */
@media (max-width: 768px) {
  .footer-section {
    padding: 3rem 0 1.5rem;
  }
  
  .social-links {
    grid-template-columns: 1fr;
  }
  
  .links-grid {
    grid-template-columns: 1fr;
  }
  
  .newsletter-form .input-group {
    flex-direction: column;
  }
  
  .newsletter-input {
    border-radius: 25px;
    margin-bottom: 1rem;
  }
  
  .newsletter-btn {
    border-radius: 25px;
  }
  
  .footer-links {
    justify-content: center;
    margin-top: 1rem;
  }
  
  .certifications {
    justify-content: center;
  }
}

@media (max-width: 576px) {
  .footer-title {
    font-size: 1.5rem;
  }
  
  .footer-subtitle {
    font-size: 1.1rem;
  }
  
  .newsletter-section {
    padding: 1.5rem;
    text-align: center;
  }
}
</style>
