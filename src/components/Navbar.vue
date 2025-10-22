<template>
  <nav class="navbar navbar-expand-lg fixed-top custom-navbar">
    <div class="container">
      <a class="navbar-brand" href="#home">
        <img src="/logo-bg.png" alt="Chicken Rise" class="navbar-logo">
      </a>
      
      <button 
        class="navbar-toggler custom-toggler" 
        type="button" 
        data-bs-toggle="collapse" 
        data-bs-target="#navbarNav"
        aria-controls="navbarNav" 
        aria-expanded="false" 
        aria-label="Toggle navigation"
      >
        <span class="toggler-icon"></span>
        <span class="toggler-icon"></span>
        <span class="toggler-icon"></span>
      </button>
      
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <a class="nav-link smooth-scroll" href="#home">
              <i class="fas fa-home me-1"></i>
              Inicio
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link smooth-scroll" href="#about">
              <i class="fas fa-users me-1"></i>
              Nosotros
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link smooth-scroll" href="#takeaway">
              <i class="fas fa-shopping-bag me-1"></i>
              Take-Away
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link smooth-scroll" href="#location">
              <i class="fas fa-map-marker-alt me-1"></i>
              Ubicación
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link smooth-scroll contact-btn" href="#contact">
              <i class="fas fa-phone me-1"></i>
              Contacto
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue'

onMounted(() => {
  // Smooth scrolling for navigation links
  const links = document.querySelectorAll('.smooth-scroll')
  links.forEach(link => {
    link.addEventListener('click', (e) => {
      e.preventDefault()
      const targetId = link.getAttribute('href')
      const targetElement = document.querySelector(targetId)
      if (targetElement) {
        const offsetTop = targetElement.offsetTop - 80 // Account for fixed navbar
        window.scrollTo({
          top: offsetTop,
          behavior: 'smooth'
        })
      }
      // Close mobile navbar after clicking a link
      const navbarCollapse = document.querySelector('#navbarNav')
      const navbarToggler = document.querySelector('.navbar-toggler')
      if (navbarCollapse.classList.contains('show')) {
        navbarToggler.click()
      }
    })
  })

  // Navbar scroll effect
  const navbar = document.querySelector('.custom-navbar')
  const handleScroll = () => {
    if (window.scrollY > 50) {
      navbar.classList.add('scrolled')
    } else {
      navbar.classList.remove('scrolled')
    }
  }

  // Close navbar when clicking outside
  const handleClickOutside = (event) => {
    const navbarCollapse = document.querySelector('#navbarNav')
    const navbarToggler = document.querySelector('.navbar-toggler')
    const navbar = document.querySelector('.custom-navbar')
    
    // Check if navbar is open and click is outside navbar
    if (navbarCollapse.classList.contains('show') && 
        !navbar.contains(event.target)) {
      navbarToggler.click()
    }
  }

  window.addEventListener('scroll', handleScroll)
  document.addEventListener('click', handleClickOutside)
  
  // Cleanup function
  onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
    document.removeEventListener('click', handleClickOutside)
  })
})
</script>

<style scoped>
.custom-navbar {
  /* background: linear-gradient(135deg, rgba(0, 0, 0, 0) 0%, rgba(26, 26, 26, 0.95) 100%); */
  /* backdrop-filter: blur(10px); */
  /* border-bottom: 2px solid transparent; */
  /* border-image: linear-gradient(90deg, #dc3545, #ffc107, #dc3545) 1; */
  padding: 1rem 0;
  transition: all 0.3s ease;
  /* box-shadow: 0 2px 20px rgba(0, 0, 0, 0.3); */
}

.custom-navbar.scrolled {
  background: linear-gradient(135deg, rgba(0, 0, 0, 0.301) 0%, rgba(26, 26, 26, 0.98) 100%);
  padding: 0.5rem 0;
  backdrop-filter: blur(10px);
  border-bottom: 2px solid transparent;
  border-image: linear-gradient(90deg, #dc3545, #ffc107, #dc3545) 1;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.4);
}

.custom-navbar.scrolled .navbar-logo {
  height: 100px;
}

.navbar-brand {
  padding: 0;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
}

.navbar-brand:hover {
  transform: scale(1.02);
}

.navbar-logo {
  height: 180px;
  width: auto;
  transition: all 0.3s ease;
  filter: brightness(1.1) contrast(1.1);
  border-radius: 8px;
}

.navbar-brand:hover .navbar-logo {
  filter: brightness(1.3) contrast(1.2) drop-shadow(0 0 15px rgba(255, 193, 7, 0.4));
  transform: rotate(2deg);
}

.navbar-nav {
  gap: 0.5rem;
}

.nav-link {
  color: #fff !important;
  font-family: 'Inter', sans-serif;
  font-weight: 600;
  font-size: 1.95rem;
  padding: 0.7rem 1.2rem !important;
  border-radius: 25px;
  transition: all 0.3s ease;
  position: relative;
  display: flex;
  align-items: center;
  text-transform: uppercase;
  letter-spacing: 0.8px;
  margin: 0 0.2rem;
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
}

.nav-link:hover {
  color: #ffc107 !important;
  background: rgba(255, 193, 7, 0.2);
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(255, 193, 7, 0.3);
  border: 1px solid rgba(255, 193, 7, 0.3);
}

.nav-link i {
  font-size: 1.9rem;
  transition: transform 0.3s ease;
}

.nav-link:hover i {
  transform: scale(1.2);
}

.contact-btn {
  background: linear-gradient(45deg, #dc3545, #c82333);
  color: #fff !important;
  margin-left: 0.5rem;
  border: 2px solid transparent;
}

.contact-btn:hover {
  background: linear-gradient(45deg, #c82333, #a71e2a);
  color: #fff !important;
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(220, 53, 69, 0.4);
}

.custom-toggler {
  border: none;
  padding: 0.5rem;
  background: transparent;
  position: relative;
  width: 35px;
  height: 35px;
}

.custom-toggler:focus {
  box-shadow: none;
}

.toggler-icon {
  display: block;
  width: 25px;
  height: 3px;
  background: #fff;
  margin: 5px 0;
  border-radius: 3px;
  transition: all 0.3s ease;
}

.custom-toggler:hover .toggler-icon {
  background: #ffffff;
}

.custom-toggler[aria-expanded="true"] .toggler-icon:nth-child(1) {
  transform: rotate(45deg) translate(6px, 6px);
}

.custom-toggler[aria-expanded="true"] .toggler-icon:nth-child(2) {
  opacity: 0;
}

.custom-toggler[aria-expanded="true"] .toggler-icon:nth-child(3) {
  transform: rotate(-45deg) translate(8px, -8px);
}

/* Mobile Styles */
@media (max-width: 991.98px) {
  .custom-navbar {
    padding: 0.8rem 0;
  }
  
  .navbar-logo {
    height: 85px;
  }
  
  .navbar-collapse {
    background: linear-gradient(135deg, rgba(0, 0, 0, 0.98) 0%, rgba(26, 26, 26, 0.98) 100%);
    border-radius: 15px;
    margin-top: 1rem;
    padding: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  }
  
  .nav-link {
    text-align: center;
    margin: 0.3rem 0;
    border-radius: 15px;
  }
  
  .contact-btn {
    margin-left: 0;
    margin-top: 0.5rem;
  }
}

@media (max-width: 576px) {
  .navbar-logo {
    height: 85px;
  }
  
  .nav-link {
    padding: 0.6rem 1rem !important;
  }
}

/* Navbar scroll effect */
@media (min-width: 992px) {
  .navbar-nav .nav-link::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 0;
    height: 2px;
    background: linear-gradient(90deg, #dc3545, #ffc107);
    transition: all 0.3s ease;
    border-radius: 1px;
  }
  
  .navbar-nav .nav-link:hover::before {
    width: 80%;
    left: 10%;
  }
  
  .contact-btn::before {
    display: none;
  }
}
</style>
