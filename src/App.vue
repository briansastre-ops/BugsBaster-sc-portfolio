<template>
  <div class="portfolio-container">
    <!-- Fondo animado en cuadrícula -->
    <div class="bg-grid"></div>
    
    <!-- Encabezado -->
    <header class="header">
      <div class="logo">
        <span class="logo-bracket">&lt;</span>
        <span class="logo-text">BugsBasters</span>
        <span class="logo-bracket">/&gt;</span>
      </div>
      <nav class="nav">
        <button @click="selectedMember = null" class="nav-link" :class="{ active: !selectedMember }">
          Equipo
        </button>
      </nav>
    </header>

    <!-- Contenido principal -->
    <main class="main-content">
      <!-- Vista de cuadrícula del equipo -->
      <transition name="fade">
        <div v-if="!selectedMember" class="team-view">
          <div class="hero-section">
            <h1 class="hero-title">
              <span class="title-line">Conoce a nuestro</span>
              <span class="title-line gradient-text">Colectivo Tecnológico</span>
            </h1>
            <p class="hero-subtitle">
              Ocho mentes brillantes construyendo el futuro de la tecnología
            </p>
          </div>

          <div class="team-grid">
            <div
              v-for="(member, index) in teamMembers"
              :key="member.id"
              class="member-card"
              :style="{ animationDelay: `${index * 0.1}s` }"
              @click="selectMember(member)"
            >
              <div class="card-inner">
                <div class="card-glow"></div>
                <div class="card-content">
                  <div class="member-avatar">
                    <div class="avatar-ring"></div>
                    <span class="avatar-text">{{ member.initials }}</span>
                  </div>
                  <h3 class="member-name">{{ member.name }}</h3>
                  <p class="member-role">{{ member.role }}</p>
                  <div class="card-footer">
                    <span class="view-profile">Ver Perfil →</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition>

      <!-- Vista de perfil individual -->
      <transition name="slide">
        <div v-if="selectedMember" class="profile-view">
          <button @click="selectedMember = null" class="back-button">
            <span class="back-arrow">←</span> Volver al Equipo
          </button>

          <div class="profile-container">
            <div class="profile-header">
              <div class="profile-avatar-large">
                <div class="avatar-ring-large"></div>
                <span class="avatar-text-large">{{ selectedMember.initials }}</span>
              </div>
              
              <div class="profile-intro">
                <h1 class="profile-name">{{ selectedMember.name }}</h1>
                <p class="profile-role">{{ selectedMember.role }}</p>
                <div class="profile-meta">
                  <span class="meta-item">
                    <span class="meta-label">Edad:</span>
                    <span class="meta-value">{{ selectedMember.age }}</span>
                  </span>
                  <span class="meta-divider">|</span>
                  <span class="meta-item">
                    <span class="meta-label">Ubicación:</span>
                    <span class="meta-value">{{ selectedMember.location }}</span>
                  </span>
                </div>
              </div>
            </div>

            <div class="profile-grid">
              <!-- Sección de estudios -->
              <div class="profile-section studies-section">
                <div class="section-header">
                  <div class="section-icon">🎓</div>
                  <h2 class="section-title">Educación y Estudios</h2>
                </div>
                <div class="section-content">
                  <div
                    v-for="(study, index) in selectedMember.studies"
                    :key="index"
                    class="study-item"
                  >
                    <div class="study-degree">{{ study.degree }}</div>
                    <div class="study-institution">{{ study.institution }}</div>
                    <div class="study-year">{{ study.year }}</div>
                  </div>
                </div>
              </div>

              <!-- Sección de habilidades -->
              <div class="profile-section skills-section">
                <div class="section-header">
                  <div class="section-icon">⚡</div>
                  <h2 class="section-title">Habilidades Principales</h2>
                </div>
                <div class="section-content">
                  <div class="skills-grid">
                    <span
                      v-for="(skill, index) in selectedMember.skills"
                      :key="index"
                      class="skill-tag"
                    >
                      {{ skill }}
                    </span>
                  </div>
                </div>
              </div>

              <!-- Sección de biografía -->
              <div class="profile-section bio-section">
                <div class="section-header">
                  <div class="section-icon">💡</div>
                  <h2 class="section-title">Acerca de</h2>
                </div>
                <div class="section-content">
                  <p class="bio-text">{{ selectedMember.bio }}</p>
                </div>
              </div>

              <!-- Sección de redes sociales -->
              <div class="profile-section social-section">
                <div class="section-header">
                  <div class="section-icon">🔗</div>
                  <h2 class="section-title">Conectar</h2>
                </div>
                <div class="section-content">
                  <div class="social-links">
                    <a
                      v-for="(link, platform) in selectedMember.social"
                      :key="platform"
                      :href="link"
                      target="_blank"
                      class="social-link"
                    >
                      <span class="social-icon">{{ getSocialIcon(platform) }}</span>
                      <span class="social-name">{{ platform }}</span>
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </main>

    <!-- Pie de página -->
    <footer class="footer">
      <p>&copy; 2025 TechCollective. Innovando el futuro.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const selectedMember = ref(null)

const teamMembers = ref([
  {
     
    id: 1,
    name: 'Brian Sastre',
    initials: 'BS',
    age: 23,
    role: 'Desarrollador Front-End | Técnico Electromecánico',
    location: 'Entre Rios, Concepción del Uruguay, Argentina',
    bio: 'Soy Técnico Electromecánico con un fuerte interés en el Front-End y una sólida formación en programación. Mi experiencia académica en la Escuela Técnica N° 2 Francisco Ramírez y mi continuo compromiso con el aprendizaje me han preparado para enfrentar desafíos en el desarrollo web. Soy proactivo, creativo y orientado a resultados, con habilidades avanzadas en React y TypeScript. Mi formación técnica me proporciona una perspectiva única para resolver problemas complejos y crear soluciones innovadoras.',
    studies: [
      { degree: 'Técnico Electromecánico', institution: 'Escuela Técnica N° 2 Francisco Ramírez', year: 'Egresado' },
      { degree: 'Tecnicatura en Programación', institution: 'UTN San Rafael', year: 'En curso' }
    ],
    skills: [
      'React', 'TypeScript', 'HTML', 'CSS', 'JavaScript', 'Next.js',
      'Python', 'Flask', 'SQL', 'Accesibilidad Web', 'Unit Testing'
    ],
    social: {
      GitHub: 'https://github.com/briansastre-ops',
      LinkedIn: 'https://www.linkedin.com/in/brian-sastre-a137452a5/',
      Portafolio: 'https://briansastre-portfolio.vercel.app/',
    },
    stats: {
      tecnologias: '10+',
      proyectos: '3+',
      dedicacion: '100%'
    }
  },
  {
    id: 2,
    name: 'Candelaria Ribotta',
    initials: 'CR',
    age: 18,
    role: 'Futura Desarrolladora y Diseñadora de Experiencias Digitales',
    location: 'San Rafael, Mendoza, Argentina',
    bio: 'Actualmente estudio la Tecnicatura en Programación en la Universidad Tecnológica Nacional de San Rafael, donde desarrollo habilidades en los distintos lenguajes de programación. Me apasiona combinar el diseño y la lógica para crear interfaces funcionales y visualmente atractivas. Disfruto del proceso creativo y técnico detrás de cada experiencia digital, desde la idea hasta el resultado final.',
    studies: [
      { degree: 'Tecnicatura en Programación', institution: 'UTN San Rafael', year: 'En curso' },
    ],
    skills: ['Python', 'Java', 'JavaScript', 'HTML', 'CSS', 'Pseint'],
    social: {
      GitHub: 'https://github.com/ribcande13',
      LinkedIn: 'https://www.linkedin.com/in/cande-ribotta-072b9736a/',
      Instagram: 'https://www.instagram.com/canddribotta/'
    }
  },
  {
    id: 3,
    name: 'Lourdes Eschler',
    initials: 'LE',
    age: 19,
    role:'Estudiante en Desarrollo y Diseño de software',
    location: 'San Rafael, Mendoza, Argentina',
    bio: 'Soy estudiante de Programación en la Universidad Tecnológica Nacional(UTN), con entusiasmo por la tecnología y el desarrollo de software. Me interesa especialmente el desarrollo web y el diseño del mismo. Recientemente descubrí mi pasión por combinar la creatividad con la tecnología. Me interesa especialmente el desarrollo de videojuegos, el diseño visual y explorar cómo el arte puede enriquecer el mundo del software. ',
    studies: [
      { degree: 'Tecnicatura en Programación', institution: 'UTN San Rafael', year: 'En curso' },
    ],
    skills: ['Python', 'Java', 'JavaScript', 'HTML', 'CSS', 'Pseint'],
    social: {
      GitHub: 'https://github.com/Luu102',
      LinkedIn: 'https://www.linkedin.com/in/lourdes-eschler-b0bb9436a',
      Instagram: 'https://www.instagram.com/lourdes.__7/'
    }
  },
  {
    id: 4,
    name: 'Rodrigo Funes',
    initials: 'RF',
    age: 29,
    role: 'Desarrollador de software | Analista funcional ',
    location: 'Ciudad Autónoma de Buenos Aires, Buenos Aires, Argentinagg',
    bio: 'Desarrollador de software y analista funcional orientado a los detalles, con experiencia práctica en análisis de datos, mejora de procesos y desarrollo web utilizando JavaScript, Python, SQL y Git. Fuertes habilidades de comunicación y experiencia trabajando en equipos ágiles con múltiples áreas. Apasionado por el aprendizaje continuo y por resolver problemas reales mediante soluciones tecnológicas.',
    studies: [
      { degree: 'Tecnicatura Universitaria en Programación', institution: 'UTN San Rafael', year: 'En curso' },
    ],
    skills: ['Python', 'JavaScript', 'SQL', 'Java', 'SQL Server', 'Vue.js', 'Express.js', 'Metodologías Ágiles'],
    social: {
      GitHub: 'https://github.com/RodrigoFunes',
      LinkedIn: 'https://www.linkedin.com/in/rodrigo-funes-809a06182/'
    }
  },
  {id: 5,
    name: 'Ian Ditlevsen',
    initials: 'ID',
    age: 26,
    role: 'Desarrollador de Software',
    location: 'San Rafael, Mendoza, Argentina',
    bio: 'Soy estudiante en programacion en la universidad de la UTN de San Rafael actualmente terminando el primer año.',
    studies: [
      { degree: 'Tecnicatura Universitaria en Programación', institution: 'UTN San Rafael', year: 'En curso' },
    ],
    skills: ['Python', 'Java', 'JavaScript', 'HTML', 'CSS'],
    social: {
      GitHub: 'https://github.com/Ditlevsen-77',
    }
  }
  // ... continúa igual para los demás miembros
])

const selectMember = (member) => {
  selectedMember.value = member
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const getSocialIcon = (platform) => {
  const icons = {
    GitHub: '⚡',
    LinkedIn: '💼',
    Twitter: '🐦',
    Portafolio: '🌐',
    Dribbble: '🎨',
    Behance: '🎭',
    Instagram: '📸',
    Medium: '✍️',
    CodePen: '🖊️',
    Kaggle: '📊'
  }
  return icons[platform] || '🔗'
}
</script>

<style>
/* ===== RESET GLOBAL ===== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  margin: 0;
  padding: 0;
  background-color: #0a0a0a;
}

body {
  margin: 0;
  padding: 0;
  background-color: #0a0a0a;
  overflow-x: hidden;
}
</style>

<style scoped>
/* ===== ESTILOS GENERALES ===== */
.portfolio-container {
  position: relative;
  min-height: 100vh;
  width: 100%;
  background: radial-gradient(circle at top left, #0a0a0a, #121212 60%, #1e1e1e);
  color: #f5f5f5;
  font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  overflow-x: hidden;
  margin: 0;
  padding: 0;
}

/* Fondo con cuadrícula animada */
.bg-grid {
  position: absolute;
  inset: 0;
  background-image: 
    linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px),
    linear-gradient(rgba(255,255,255,0.05) 1px, transparent 1px);
  background-size: 40px 40px;
  animation: gridMove 10s linear infinite;
  z-index: 0;
}

@keyframes gridMove {
  from { background-position: 0 0; }
  to { background-position: 40px 40px; }
}

/* ===== HEADER ===== */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 1.5rem;
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(0,0,0,0.8);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255,255,255,0.1);
}

.logo {
  display: flex;
  align-items: center;
  font-weight: 600;
  font-size: clamp(1rem, 2.5vw, 1.2rem);
}

.logo-bracket {
  color: #00ffc3;
  font-weight: bold;
}

.logo-text {
  margin: 0 0.4rem;
  letter-spacing: 0.5px;
}

.nav {
  display: flex;
  gap: 1rem;
}

.nav-link {
  background: transparent;
  color: #f5f5f5;
  border: none;
  cursor: pointer;
  font-size: clamp(0.875rem, 2vw, 1rem);
  padding: 0.5rem 1rem;
  border-radius: 6px;
  transition: all 0.3s;
}

.nav-link:hover {
  background: rgba(0,255,195,0.1);
  color: #00ffc3;
}

.nav-link.active {
  color: #00ffc3;
  background: rgba(0,255,195,0.15);
}

/* ===== CONTENIDO PRINCIPAL ===== */
.main-content {
  position: relative;
  z-index: 5;
  padding: clamp(1.5rem, 4vw, 3rem) clamp(1rem, 3vw, 2rem);
  max-width: 1400px;
  margin: 0 auto;
}

/* ===== SECCIÓN HERO ===== */
.hero-section {
  text-align: center;
  margin-bottom: clamp(2rem, 5vw, 3rem);
  padding: 1rem 0;
}

.hero-title {
  font-size: clamp(1.75rem, 5vw, 2.5rem);
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.title-line {
  display: block;
  margin: 0.3rem 0;
}

.gradient-text {
  background: linear-gradient(90deg, #00ffc3, #00bfff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  color: #ccc;
  font-size: clamp(0.875rem, 2.5vw, 1.1rem);
  margin-top: 0.5rem;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

/* ===== GRID DEL EQUIPO ===== */
.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(100%, 260px), 1fr));
  gap: clamp(1.5rem, 3vw, 2rem);
  justify-items: center;
}

.member-card {
  position: relative;
  width: 100%;
  max-width: 320px;
  background: rgba(255,255,255,0.05);
  border-radius: 16px;
  padding: clamp(1.5rem, 3vw, 2rem);
  cursor: pointer;
  transition: all 0.4s ease;
  text-align: center;
  overflow: hidden;
  animation: fadeUp 0.6s ease forwards;
  transform: translateY(10px);
  opacity: 0;
  border: 1px solid rgba(255,255,255,0.05);
}

@keyframes fadeUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.member-card:hover {
  background: rgba(0,255,195,0.1);
  transform: translateY(-6px);
  box-shadow: 0 8px 24px rgba(0,255,195,0.2);
  border-color: rgba(0,255,195,0.3);
}

.card-inner {
  position: relative;
  z-index: 2;
}

.member-avatar {
  width: clamp(70px, 15vw, 80px);
  height: clamp(70px, 15vw, 80px);
  border-radius: 50%;
  background: linear-gradient(135deg, #00ffc3, #00bfff);
  color: #0a0a0a;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: clamp(1.2rem, 3vw, 1.5rem);
  margin: 0 auto 1rem auto;
  position: relative;
}

.avatar-ring {
  position: absolute;
  inset: -5px;
  border-radius: 50%;
  border: 2px solid rgba(0,255,195,0.4);
  animation: spin 4s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.member-name {
  font-weight: 600;
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  margin-bottom: 0.5rem;
}

.member-role {
  color: #aaa;
  font-size: clamp(0.85rem, 2vw, 0.95rem);
  margin-bottom: 1rem;
  line-height: 1.4;
}

.card-footer {
  margin-top: 1rem;
}

.view-profile {
  color: #00ffc3;
  font-weight: 500;
  font-size: clamp(0.85rem, 2vw, 0.95rem);
  transition: opacity 0.3s;
  opacity: 0.8;
}

.member-card:hover .view-profile {
  opacity: 1;
}

/* ===== PERFIL INDIVIDUAL ===== */
.profile-view {
  max-width: 1000px;
  margin: 0 auto;
}

.back-button {
  background: rgba(0,255,195,0.1);
  border: 1px solid rgba(0,255,195,0.3);
  color: #00ffc3;
  cursor: pointer;
  margin-bottom: 1.5rem;
  font-size: clamp(0.9rem, 2vw, 1rem);
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  transition: all 0.3s;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

.back-button:hover {
  background: rgba(0,255,195,0.2);
  transform: translateX(-4px);
}

.back-arrow {
  font-size: 1.2rem;
}

.profile-container {
  background: rgba(255,255,255,0.05);
  border-radius: 18px;
  padding: clamp(1.5rem, 4vw, 2.5rem);
  box-shadow: 0 0 30px rgba(0,255,195,0.1);
  border: 1px solid rgba(255,255,255,0.08);
}

.profile-header {
  display: flex;
  align-items: center;
  gap: clamp(1.5rem, 4vw, 2.5rem);
  flex-wrap: wrap;
  margin-bottom: 2rem;
}

.profile-avatar-large {
  width: clamp(100px, 20vw, 130px);
  height: clamp(100px, 20vw, 130px);
  border-radius: 50%;
  background: linear-gradient(135deg, #00ffc3, #00bfff);
  color: #0a0a0a;
  font-size: clamp(1.5rem, 4vw, 2.2rem);
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  flex-shrink: 0;
}

.avatar-ring-large {
  position: absolute;
  inset: -6px;
  border-radius: 50%;
  border: 3px solid rgba(0,255,195,0.3);
  animation: spin 5s linear infinite;
}

.profile-intro {
  flex: 1;
  min-width: 250px;
}

.profile-name {
  font-size: clamp(1.5rem, 4vw, 2rem);
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.profile-role {
  color: #ccc;
  font-size: clamp(0.95rem, 2.5vw, 1.1rem);
  line-height: 1.4;
  margin-bottom: 0.75rem;
}

.profile-meta {
  color: #aaa;
  font-size: clamp(0.85rem, 2vw, 0.95rem);
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  align-items: center;
}

.meta-item {
  display: flex;
  gap: 0.3rem;
}

.meta-label {
  font-weight: 500;
}

.meta-divider {
  color: rgba(255,255,255,0.3);
}

.profile-grid {
  display: grid;
  gap: clamp(1.2rem, 3vw, 1.5rem);
  margin-top: 2rem;
}

.profile-section {
  background: rgba(255,255,255,0.04);
  border-radius: 12px;
  padding: clamp(1.2rem, 3vw, 1.5rem);
  border-left: 3px solid #00ffc3;
  transition: all 0.3s;
}

.profile-section:hover {
  background: rgba(255,255,255,0.06);
  border-left-width: 5px;
}

.section-header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1rem;
}

.section-icon {
  font-size: clamp(1.2rem, 3vw, 1.4rem);
}

.section-title {
  font-weight: 600;
  font-size: clamp(1rem, 2.5vw, 1.2rem);
}

.study-item {
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid rgba(255,255,255,0.05);
}

.study-item:last-child {
  border-bottom: none;
  margin-bottom: 0;
  padding-bottom: 0;
}

.study-degree {
  font-weight: 500;
  font-size: clamp(0.95rem, 2vw, 1.05rem);
  margin-bottom: 0.3rem;
}

.study-institution,
.study-year {
  color: #aaa;
  font-size: clamp(0.85rem, 2vw, 0.9rem);
  line-height: 1.4;
}

.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: clamp(0.4rem, 1.5vw, 0.6rem);
}

.skill-tag {
  background: rgba(0,255,195,0.1);
  border: 1px solid rgba(0,255,195,0.3);
  border-radius: 8px;
  padding: 0.5rem 1rem;
  font-size: clamp(0.8rem, 2vw, 0.9rem);
  color: #00ffc3;
  transition: all 0.3s;
}

.skill-tag:hover {
  background: rgba(0,255,195,0.2);
  transform: translateY(-2px);
}

.bio-text {
  color: #ddd;
  line-height: 1.6;
  font-size: clamp(0.9rem, 2vw, 1rem);
}

.social-links {
  display: flex;
  flex-wrap: wrap;
  gap: clamp(0.8rem, 2vw, 1.2rem);
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #00ffc3;
  text-decoration: none;
  padding: 0.6rem 1rem;
  background: rgba(0,255,195,0.05);
  border: 1px solid rgba(0,255,195,0.2);
  border-radius: 8px;
  transition: all 0.3s;
  font-size: clamp(0.85rem, 2vw, 0.95rem);
}

.social-link:hover {
  background: rgba(0,255,195,0.15);
  color: #fff;
  transform: translateY(-2px);
}

.social-icon {
  font-size: 1.2rem;
}

/* ===== FOOTER ===== */
.footer {
  text-align: center;
  padding: clamp(1.5rem, 3vw, 2rem) 1rem;
  color: #777;
  font-size: clamp(0.8rem, 2vw, 0.9rem);
  border-top: 1px solid rgba(255,255,255,0.05);
}

/* ===== ANIMACIONES ===== */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: all 0.4s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

/* ===== MEDIA QUERIES ===== */

/* Tablets */
@media (max-width: 768px) {
  .header {
    padding: 1rem;
  }
  
  .team-grid {
    grid-template-columns: repeat(auto-fill, minmax(min(100%, 240px), 1fr));
    gap: 1.5rem;
  }
  
  .profile-header {
    flex-direction: column;
    text-align: center;
  }
  
  .profile-intro {
    width: 100%;
  }
  
  .profile-meta {
    justify-content: center;
  }
}

/* Móviles */
@media (max-width: 480px) {
  .header {
    padding: 0.75rem 1rem;
  }
  
  .logo {
    font-size: 1rem;
  }
  
  .nav-link {
    padding: 0.4rem 0.75rem;
    font-size: 0.9rem;
  }
  
  .main-content {
    padding: 1.5rem 1rem;
  }
  
  .hero-title {
    font-size: 1.5rem;
  }
  
  .hero-subtitle {
    font-size: 0.9rem;
  }
  
  .team-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .member-card {
    max-width: 100%;
  }
  
  .back-button {
    width: 100%;
    justify-content: center;
    padding: 0.875rem 1rem;
  }
  
  .profile-container {
    padding: 1.5rem;
  }
  
  .profile-avatar-large {
    width: 100px;
    height: 100px;
    font-size: 1.8rem;
  }
  
  .profile-name {
    font-size: 1.5rem;
  }
  
  .skills-grid {
    gap: 0.5rem;
  }
  
  .skill-tag {
    padding: 0.4rem 0.8rem;
    font-size: 0.85rem;
  }
  
  .social-links {
    gap: 0.75rem;
  }
  
  .social-link {
    flex: 1 1 calc(50% - 0.375rem);
    justify-content: center;
    min-width: 140px;
  }
}

/* Pantallas muy pequeñas */
@media (max-width: 360px) {
  .hero-title {
    font-size: 1.3rem;
  }
  
  .member-avatar {
    width: 60px;
    height: 60px;
    font-size: 1.2rem;
  }
  
  .profile-section {
    padding: 1rem;
  }
  
  .social-link {
    flex: 1 1 100%;
  }
}
</style>
