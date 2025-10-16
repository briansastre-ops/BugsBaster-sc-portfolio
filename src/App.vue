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
      LinkedIn: 'https://www.linkedin.com/in/brian-sastre/',
      Portafolio: 'https://briansastre-ops.github.io/',
    },
    stats: {
      tecnologias: '10+',
      proyectos: '3+',
      dedicacion: '100%'
    }
  },
  {
    id: 2,
    name: 'Sarah Martinez',
    initials: 'SM',
    age: 26,
    role: 'Diseñadora UI/UX',
    location: 'Nueva York, NY',
    bio: 'Diseñadora creativa enfocada en crear experiencias de usuario intuitivas y atractivas. Experta en sistemas de diseño y prototipado.',
    studies: [
      { degree: 'Lic. en Diseño Gráfico', institution: 'Parsons School of Design', year: '2020' },
      { degree: 'Certificado en UX Design', institution: 'Nielsen Norman Group', year: '2021' }
    ],
    skills: ['Figma', 'Adobe XD', 'Prototipado', 'Investigación de Usuarios', 'Sistemas de Diseño', 'Animación'],
    social: {
      Dribbble: 'https://dribbble.com',
      Behance: 'https://behance.net',
      LinkedIn: 'https://linkedin.com',
      Instagram: 'https://instagram.com'
    }
  },
  {
    id: 3,
    name: 'Marcus Johnson',
    initials: 'MJ',
    age: 30,
    role: 'Ingeniero DevOps',
    location: 'Austin, TX',
    bio: 'Entusiasta de la infraestructura y automatización. Experto en CI/CD, contenedores y plataformas en la nube. ',
    studies: [
      { degree: 'Lic. en Tecnología de la Información', institution: 'Universidad de Texas', year: '2017' },
      { degree: 'Arquitecto de Soluciones AWS', institution: 'Amazon Web Services', year: '2019' }
    ],
    skills: ['Kubernetes', 'Terraform', 'Jenkins', 'AWS', 'Linux', 'Python'],
    social: {
      GitHub: 'https://github.com',
      LinkedIn: 'https://linkedin.com',
      Medium: 'https://medium.com',
      Twitter: 'https://twitter.com'
    }
  },
  {
    id: 4,
    name: 'Emily Wong',
    initials: 'EW',
    age: 27,
    role: 'Científica de Datos',
    location: 'Seattle, WA',
    bio: 'Apasionada por el análisis de datos, machine learning y visualización. Convierte datos en estrategias accionables.',
    studies: [
      { degree: 'Lic. en Matemáticas', institution: 'UC Berkeley', year: '2019' },
      { degree: 'Maestría en Ciencia de Datos', institution: 'Carnegie Mellon', year: '2022' }
    ],
    skills: ['Python', 'TensorFlow', 'SQL', 'R', 'Tableau', 'Machine Learning'],
    social: {
      GitHub: 'https://github.com',
      LinkedIn: 'https://linkedin.com',
      Kaggle: 'https://kaggle.com',
      Twitter: 'https://twitter.com'
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

<style scoped>


html,
body {
  margin: 0;
  padding: 0;
  background-color: #000;
  overflow-x: hidden;
}


/* ===== ESTILOS GENERALES ===== */
.portfolio-container {
  position: relative;
  min-height: 100vh;
  background: radial-gradient(circle at top left, #0a0a0a, #121212 60%, #1e1e1e);
  color: #f5f5f5;
  font-family: "Inter", sans-serif;
  overflow-x: hidden;
}

/* Fondo con cuadrícula animada */
.bg-grid {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(90deg, rgba(255,255,255,0.05) 1px, transparent 1px),
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
  padding: 1.2rem 2rem;
  position: relative;
  z-index: 10;
  background: rgba(0,0,0,0.5);
  backdrop-filter: blur(6px);
  border-bottom: 1px solid rgba(255,255,255,0.1);
}

.logo {
  display: flex;
  align-items: center;
  font-weight: 600;
  font-size: 1.2rem;
}

.logo-bracket {
  color: #00ffc3;
  font-weight: bold;
}

.logo-text {
  margin: 0 6px;
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
  font-size: 1rem;
  transition: color 0.3s;
}

.nav-link.active,
.nav-link:hover {
  color: #00ffc3;
}

/* ===== SECCIÓN PRINCIPAL ===== */
.main-content {
  position: relative;
  z-index: 5;
  padding: 3rem 2rem;
}

.hero-section {
  text-align: center;
  margin-bottom: 3rem;
}

.hero-title {
  font-size: 2.2rem;
  font-weight: 700;
  line-height: 1.3;
}

.title-line {
  display: block;
}

.gradient-text {
  background: linear-gradient(90deg, #00ffc3, #00bfff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-subtitle {
  color: #ccc;
  font-size: 1rem;
  margin-top: 0.5rem;
}

/* ===== GRID DEL EQUIPO ===== */
.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  justify-items: center;
}

.member-card {
  position: relative;
  width: 100%;
  max-width: 280px;
  background: rgba(255,255,255,0.05);
  border-radius: 16px;
  padding: 2rem 1.5rem;
  cursor: pointer;
  transition: all 0.4s ease;
  text-align: center;
  overflow: hidden;
  animation: fadeUp 0.6s ease forwards;
  transform: translateY(10px);
  opacity: 0;
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
  box-shadow: 0 0 12px rgba(0,255,195,0.3);
}

.member-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background: #00ffc3;
  color: #0a0a0a;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1.5rem;
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
  from { transform: rotate(0); }
  to { transform: rotate(360deg); }
}

.member-name {
  font-weight: 600;
  font-size: 1.2rem;
}

.member-role {
  color: #aaa;
  font-size: 0.95rem;
  margin-bottom: 0.8rem;
}

.view-profile {
  color: #00ffc3;
  font-weight: 500;
  font-size: 0.95rem;
  transition: opacity 0.3s;
}

.member-card:hover .view-profile {
  opacity: 1;
}

/* ===== PERFIL INDIVIDUAL ===== */
.profile-view {
  max-width: 900px;
  margin: 0 auto;
}

.back-button {
  background: none;
  border: none;
  color: #00ffc3;
  cursor: pointer;
  margin-bottom: 1.5rem;
  font-size: 1rem;
  transition: color 0.3s;
}

.back-button:hover {
  color: #00bfff;
}

.profile-container {
  background: rgba(255,255,255,0.05);
  border-radius: 18px;
  padding: 2rem;
  box-shadow: 0 0 20px rgba(0,255,195,0.15);
}

.profile-header {
  display: flex;
  align-items: center;
  gap: 2rem;
  flex-wrap: wrap;
  justify-content: center;
}

.profile-avatar-large {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background: #00ffc3;
  color: #0a0a0a;
  font-size: 2rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.avatar-ring-large {
  position: absolute;
  inset: -6px;
  border-radius: 50%;
  border: 3px solid rgba(0,255,195,0.3);
  animation: spin 5s linear infinite;
}

.profile-name {
  font-size: 1.8rem;
  font-weight: 600;
}

.profile-role {
  color: #ccc;
  font-size: 1rem;
}

.profile-meta {
  color: #aaa;
  margin-top: 0.5rem;
  font-size: 0.9rem;
}

.meta-divider {
  margin: 0 0.5rem;
}

.profile-grid {
  display: grid;
  gap: 1.5rem;
  margin-top: 2rem;
}

.profile-section {
  background: rgba(255,255,255,0.04);
  border-radius: 12px;
  padding: 1.5rem;
  border-left: 3px solid #00ffc3;
}

.section-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.8rem;
}

.section-icon {
  font-size: 1.3rem;
}

.section-title {
  font-weight: 600;
  font-size: 1.1rem;
}

.study-item {
  margin-bottom: 0.5rem;
}

.study-degree {
  font-weight: 500;
}

.study-institution,
.study-year {
  color: #aaa;
  font-size: 0.9rem;
}

.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.skill-tag {
  background: rgba(0,255,195,0.1);
  border: 1px solid rgba(0,255,195,0.3);
  border-radius: 8px;
  padding: 0.3rem 0.7rem;
  font-size: 0.85rem;
  color: #00ffc3;
}

.bio-text {
  color: #ddd;
  line-height: 1.5;
}

.social-links {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  color: #00ffc3;
  text-decoration: none;
  transition: color 0.3s;
}

.social-link:hover {
  color: #00bfff;
}

/* ===== FOOTER ===== */
.footer {
  text-align: center;
  padding: 2rem 0;
  color: #777;
  font-size: 0.9rem;
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

/* ===== RESPONSIVE ===== */
@media (max-width: 600px) {
  .hero-title {
    font-size: 1.8rem;
  }

  .profile-header {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .profile-avatar-large {
    width: 100px;
    height: 100px;
    font-size: 1.5rem;
  }
}
</style>
