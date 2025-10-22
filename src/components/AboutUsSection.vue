<template>
    <section id="about" class="about-section">
        <div class="container">
            <div class="row align-items-center">
                <!-- Columna Izquierda - Contenido -->
                <div class="col-lg-6">
                    <div class="about-content">
                        <h2 class="about-title">SOBRE NOSOTROS</h2>

                        <div class="about-text">
                            <p class="intro-text">
                                Chicken Rise es mucho más que un restaurante, es una experiencia única para los amantes
                                del pollo.
                                Especializados en cocina halal y recetas caseras llenas de sabor, preparamos cada plato
                                con dedicación y pasión para ofrecerte una comida auténtica, fresca y de calidad.
                                <br>
                                <br>
                                Nos encontrarás en Calle Almenillas N10 Local 3 (Granada), un espacio pensado para
                                disfrutar del mejor pollo crujiente, en un ambiente acogedor y moderno. Y si prefieres
                                saborearlo en casa, puedes pedirlo fácilmente para Take-Away — el sabor de Chicken Rise
                                llega donde tú estés.
<br>
                                <br>
                                Nuestras especialidades de pollo están marinadas con nuestra receta secreta, acompañadas
                                de salsas irresistibles y guarniciones que te harán volver una y otra vez.
                                Crujiente por fuera, tierno por dentro… simplemente perfecto.

                                En local o para llevar, Chicken Rise es mucho más que pollo.


                            </p>


                            <p class="values-text">
                                ¿Y tú? ¿Ya sabes cómo vas a disfrutar tu Chicken Rise hoy?
                            </p>

                        </div>
                    </div>
                </div>

                <!-- Columna Derecha - Imagen -->
                <div class="col-lg-6">
                    <div class="about-image-container">
                        <div class="image-wrapper">
                            <img src="/about.png" alt="Nuestro restaurante Chicken Rise" class="about-image">

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
    const aboutContent = document.querySelector('.about-content')
    const aboutImage = document.querySelector('.about-image-container')

    if (aboutContent) observer.observe(aboutContent)
    if (aboutImage) observer.observe(aboutImage)
})
</script>

<style scoped>
.about-section {
    background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 50%, #1a1a1a 100%);
    padding: 6rem 0;
    position: relative;
    overflow: hidden;
}

.about-section::before {
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
.about-content {
    padding: 2rem;
    opacity: 0;
    transform: translateX(-50px);
    transition: all 0.8s ease;
}

.about-content.animate-in {
    opacity: 1;
    transform: translateX(0);
}

.about-title {
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

.about-title::after {
    content: '';
    position: absolute;
    bottom: -15px;
    left: 0;
    width: 80px;
    height: 4px;
    background: linear-gradient(90deg, #dc3545, #ffc107);
    border-radius: 2px;
}

.about-text {
    color: #e9ecef;
    line-height: 1.8;
    font-size: 1.1rem;
}

.intro-text {
    font-size: 1.25rem;
    color: #f8f9fa;
    margin-bottom: 2rem;
    font-weight: 500;
    line-height: 1.6;
}

.description-text,
.values-text {
    margin-bottom: 1.75rem;
    color: #ced4da;
    font-weight: 400;
}

.about-highlights {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-top: 2.5rem;
}

.highlight-item {
    display: flex;
    align-items: center;
    gap: 1rem;
    color: #f8f9fa;
    font-weight: 600;
    font-size: 1.1rem;
    padding: 0.75rem 0;
}

.highlight-item i {
    color: #ffc107;
    font-size: 1.3rem;
    width: 24px;
    text-align: center;
}

/* Columna Derecha - Imagen */
.about-image-container {
    position: relative;
    padding: 2rem;
    opacity: 0;
    transform: translateX(50px);
    transition: all 0.8s ease 0.3s;
}

.about-image-container.animate-in {
    opacity: 1;
    transform: translateX(0);
}

.image-wrapper {
    position: relative;
    border-radius: 20px;
    overflow: hidden;
    box-shadow:
        0 20px 40px rgba(0, 0, 0, 0.4),
        0 0 0 8px rgba(255, 193, 7, 0.1);
    transform: perspective(1000px) rotateY(-5deg);
    transition: transform 0.5s ease;
}

.image-wrapper:hover {
    transform: perspective(1000px) rotateY(0deg) scale(1.02);
}

.about-image {
    width: 100%;
    height: 400px;
    object-fit: cover;
    display: block;
    filter: brightness(0.9) contrast(1.1) saturate(1.1);
    transition: filter 0.3s ease;
}

.image-wrapper:hover .about-image {
    filter: brightness(1) contrast(1.2) saturate(1.2);
}

.image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg,
            rgba(220, 53, 69, 0.8) 0%,
            rgba(0, 0, 0, 0.3) 50%,
            rgba(255, 193, 7, 0.6) 100%);
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

.play-icon {
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

    0%,
    100% {
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
    .about-section {
        padding: 4rem 0;
    }

    .about-content,
    .about-image-container {
        padding: 1.5rem;
        text-align: center;
    }

    .about-title {
        margin-bottom: 2rem;
    }

    .about-title::after {
        left: 50%;
        transform: translateX(-50%);
    }

    .image-wrapper {
        transform: none;
        margin-top: 2rem;
    }

    .about-highlights {
        justify-content: center;
        align-items: center;
    }
}

@media (max-width: 768px) {
    .about-section {
        padding: 3rem 0;
    }

    .about-content,
    .about-image-container {
        padding: 1rem;
    }

    .about-title {
        font-size: 2rem;
        letter-spacing: 2px;
    }

    .about-text {
        font-size: 1rem;
    }

    .intro-text {
        font-size: 1.1rem;
    }

    .about-image {
        height: 300px;
    }

    .highlight-item {
        font-size: 1rem;
    }
}

@media (max-width: 576px) {
    .about-section {
        padding: 2rem 0;
    }

    .about-title {
        font-size: 1.8rem;
        letter-spacing: 1px;
        margin-bottom: 1.5rem;
    }

    .about-image {
        height: 250px;
    }

    .highlight-item {
        font-size: 0.95rem;
        gap: 0.75rem;
    }

    .decorative-elements {
        display: none;
    }
}
</style>
