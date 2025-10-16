<template>
  <div class="portfolio-container">
    <!-- Animated background grid -->
    <div class="bg-grid"></div>
    
    <!-- Header -->
    <header class="header">
      <div class="logo">
        <span class="logo-bracket">&lt;</span>
        <span class="logo-text">TechCollective</span>
        <span class="logo-bracket">/&gt;</span>
      </div>
      <nav class="nav">
        <button @click="selectedMember = null" class="nav-link" :class="{ active: !selectedMember }">
          Team
        </button>
      </nav>
    </header>

    <!-- Main Content -->
    <main class="main-content">
      <!-- Team Grid View -->
      <transition name="fade">
        <div v-if="!selectedMember" class="team-view">
          <div class="hero-section">
            <h1 class="hero-title">
              <span class="title-line">Meet Our</span>
              <span class="title-line gradient-text">Tech Collective</span>
            </h1>
            <p class="hero-subtitle">
              Eight brilliant minds crafting the future of technology
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
                    <span class="view-profile">View Profile →</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition>

      <!-- Profile Detail View -->
      <transition name="slide">
        <div v-if="selectedMember" class="profile-view">
          <button @click="selectedMember = null" class="back-button">
            <span class="back-arrow">←</span> Back to Team
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
                    <span class="meta-label">Age:</span>
                    <span class="meta-value">{{ selectedMember.age }}</span>
                  </span>
                  <span class="meta-divider">|</span>
                  <span class="meta-item">
                    <span class="meta-label">Location:</span>
                    <span class="meta-value">{{ selectedMember.location }}</span>
                  </span>
                </div>
              </div>
            </div>

            <div class="profile-grid">
              <!-- Studies Section -->
              <div class="profile-section studies-section">
                <div class="section-header">
                  <div class="section-icon">🎓</div>
                  <h2 class="section-title">Education & Studies</h2>
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

              <!-- Skills Section -->
              <div class="profile-section skills-section">
                <div class="section-header">
                  <div class="section-icon">⚡</div>
                  <h2 class="section-title">Core Skills</h2>
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

              <!-- Bio Section -->
              <div class="profile-section bio-section">
                <div class="section-header">
                  <div class="section-icon">💡</div>
                  <h2 class="section-title">About</h2>
                </div>
                <div class="section-content">
                  <p class="bio-text">{{ selectedMember.bio }}</p>
                </div>
              </div>

              <!-- Social Links Section -->
              <div class="profile-section social-section">
                <div class="section-header">
                  <div class="section-icon">🔗</div>
                  <h2 class="section-title">Connect</h2>
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

    <!-- Footer -->
    <footer class="footer">
      <p>&copy; 2025 TechCollective. Innovating the future.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const selectedMember = ref(null)

const teamMembers = ref([
  {
    id: 1,
    name: 'Alex Chen',
    initials: 'AC',
    age: 28,
    role: 'Full Stack Developer',
    location: 'San Francisco, CA',
    bio: 'Passionate about building scalable web applications with modern technologies. Specializes in React, Node.js, and cloud architecture. Always exploring new frameworks and best practices.',
    studies: [
      { degree: 'B.S. Computer Science', institution: 'Stanford University', year: '2019' },
      { degree: 'M.S. Software Engineering', institution: 'MIT', year: '2021' }
    ],
    skills: ['React', 'Node.js', 'TypeScript', 'AWS', 'Docker', 'GraphQL'],
    social: {
      GitHub: 'https://github.com',
      LinkedIn: 'https://linkedin.com',
      Twitter: 'https://twitter.com',
      Portfolio: 'https://example.com'
    }
  },
  {
    id: 2,
    name: 'Sarah Martinez',
    initials: 'SM',
    age: 26,
    role: 'UI/UX Designer',
    location: 'New York, NY',
    bio: 'Creative designer focused on crafting intuitive and beautiful user experiences. Expert in design systems, prototyping, and user research. Believes design should be both functional and delightful.',
    studies: [
      { degree: 'B.A. Graphic Design', institution: 'Parsons School of Design', year: '2020' },
      { degree: 'UX Design Certificate', institution: 'Nielsen Norman Group', year: '2021' }
    ],
    skills: ['Figma', 'Adobe XD', 'Prototyping', 'User Research', 'Design Systems', 'Animation'],
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
    role: 'DevOps Engineer',
    location: 'Austin, TX',
    bio: 'Infrastructure enthusiast dedicated to automating deployments and ensuring system reliability. Expert in CI/CD pipelines, containerization, and cloud platforms. Passionate about infrastructure as code.',
    studies: [
      { degree: 'B.S. Information Technology', institution: 'University of Texas', year: '2017' },
      { degree: 'AWS Solutions Architect', institution: 'Amazon Web Services', year: '2019' }
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
    role: 'Data Scientist',
    location: 'Seattle, WA',
    bio: 'Data-driven problem solver leveraging machine learning and analytics to extract insights. Specializes in predictive modeling, data visualization, and statistical analysis. Loves turning data into actionable strategies.',
    studies: [
      { degree: 'B.S. Mathematics', institution: 'UC Berkeley', year: '2019' },
      { degree: 'M.S. Data Science', institution: 'Carnegie Mellon', year: '2022' }
    ],
    skills: ['Python', 'TensorFlow', 'SQL', 'R', 'Tableau', 'Machine Learning'],
    social: {
      GitHub: 'https://github.com',
      LinkedIn: 'https://linkedin.com',
      Kaggle: 'https://kaggle.com',
      Twitter: 'https://twitter.com'
    }
  },
  {
    id: 5,
    name: 'David Kim',
    initials: 'DK',
    age: 29,
    role: 'Mobile Developer',
    location: 'Los Angeles, CA',
    bio: 'Mobile-first developer creating seamless experiences across iOS and Android platforms. Expert in React Native and native development. Focused on performance optimization and user engagement.',
    studies: [
      { degree: 'B.S. Computer Engineering', institution: 'UCLA', year: '2018' },
      { degree: 'iOS Development Bootcamp', institution: 'App Academy', year: '2019' }
    ],
    skills: ['React Native', 'Swift', 'Kotlin', 'Firebase', 'Redux', 'Mobile UI'],
    social: {
      GitHub: 'https://github.com',
      LinkedIn: 'https://linkedin.com',
      Twitter: 'https://twitter.com',
      Portfolio: 'https://example.com'
    }
  },
  {
    id: 6,
    name: 'Jessica Taylor',
    initials: 'JT',
    age: 25,
    role: 'Frontend Developer',
    location: 'Boston, MA',
    bio: 'Frontend specialist passionate about creating performant and accessible web applications. Expert in modern JavaScript frameworks and CSS architecture. Advocates for web standards and best practices.',
    studies: [
      { degree: 'B.S. Web Development', institution: 'Northeastern University', year: '2021' },
      { degree: 'Frontend Masters Certificate', institution: 'Frontend Masters', year: '2022' }
    ],
    skills: ['Vue.js', 'React', 'CSS', 'JavaScript', 'Webpack', 'Accessibility'],
    social: {
      GitHub: 'https://github.com',
      CodePen: 'https://codepen.io',
      LinkedIn: 'https://linkedin.com',
      Twitter: 'https://twitter.com'
    }
  },
  {
    id: 7,
    name: 'Ryan Patel',
    initials: 'RP',
    age: 31,
    role: 'Security Engineer',
    location: 'Chicago, IL',
    bio: 'Cybersecurity expert focused on protecting applications and infrastructure from threats. Specializes in penetration testing, security audits, and secure coding practices. Committed to building secure systems.',
    studies: [
      { degree: 'B.S. Cybersecurity', institution: 'Purdue University', year: '2016' },
      { degree: 'CISSP Certification', institution: 'ISC²', year: '2018' }
    ],
    skills: ['Penetration Testing', 'Security Audits', 'Cryptography', 'Network Security', 'Python', 'Ethical Hacking'],
    social: {
      GitHub: 'https://github.com',
      LinkedIn: 'https://linkedin.com',
      Twitter: 'https://twitter.com',
      Medium: 'https://medium.com'
    }
  },
  {
    id: 8,
    name: 'Olivia Brown',
    initials: 'OB',
    age: 26,
    role: 'Product Manager',
    location: 'Denver, CO',
    bio: 'Strategic product leader bridging technology and business needs. Expert in agile methodologies, user stories, and product roadmaps. Passionate about delivering value and driving innovation.',
    studies: [
      { degree: 'B.A. Business Administration', institution: 'University of Colorado', year: '2020' },
      { degree: 'Product Management Certificate', institution: 'Product School', year: '2021' }
    ],
    skills: ['Agile', 'Scrum', 'Product Strategy', 'User Stories', 'Analytics', 'Roadmapping'],
    social: {
      LinkedIn: 'https://linkedin.com',
      Twitter: 'https://twitter.com',
      Medium: 'https://medium.com',
      Portfolio: 'https://example.com'
    }
  }
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
    Portfolio: '🌐',
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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.portfolio-container {
  min-height: 100vh;
  background: #0a0e27;
  color: #e4e4e7;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  position: relative;
  overflow-x: hidden;
}

/* Animated Background Grid */
.bg-grid {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(rgba(6, 182, 212, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(6, 182, 212, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 20s linear infinite;
  pointer-events: none;
  z-index: 0;
}

@keyframes gridMove {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(50px, 50px);
  }
}

/* Header */
.header {
  position: relative;
  z-index: 10;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  border-bottom: 1px solid rgba(6, 182, 212, 0.2);
  backdrop-filter: blur(10px);
  background: rgba(10, 14, 39, 0.8);
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.logo-bracket {
  color: #06b6d4;
  font-weight: 400;
}

.logo-text {
  background: linear-gradient(135deg, #06b6d4 0%, #3b82f6 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-link {
  background: none;
  border: 1px solid rgba(6, 182, 212, 0.3);
  color: #e4e4e7;
  padding: 0.5rem 1.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 0.95rem;
}

.nav-link:hover,
.nav-link.active {
  background: rgba(6, 182, 212, 0.1);
  border-color: #06b6d4;
  box-shadow: 0 0 20px rgba(6, 182, 212, 0.3);
}

/* Main Content */
.main-content {
  position: relative;
  z-index: 1;
  padding: 2rem;
  max-width: 1400px;
  margin: 0 auto;
}

/* Hero Section */
.hero-section {
  text-align: center;
  margin-bottom: 4rem;
  padding: 2rem 0;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 800;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.title-line {
  display: block;
}

.gradient-text {
  background: linear-gradient(135deg, #06b6d4 0%, #3b82f6 50%, #8b5cf6 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradientShift 3s ease infinite;
}

@keyframes gradientShift {
  0%, 100% {
    filter: hue-rotate(0deg);
  }
  50% {
    filter: hue-rotate(10deg);
  }
}

.hero-subtitle {
  font-size: 1.25rem;
  color: #a1a1aa;
  max-width: 600px;
  margin: 0 auto;
}

/* Team Grid */
.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.member-card {
  animation: fadeInUp 0.6s ease forwards;
  opacity: 0;
  cursor: pointer;
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
  from {
    opacity: 0;
    transform: translateY(20px);
  }
}

.card-inner {
  position: relative;
  background: rgba(15, 23, 42, 0.6);
  border: 1px solid rgba(6, 182, 212, 0.2);
  border-radius: 1rem;
  padding: 2rem;
  transition: all 0.4s ease;
  backdrop-filter: blur(10px);
  overflow: hidden;
}

.card-glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(6, 182, 212, 0.1) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.member-card:hover .card-inner {
  transform: translateY(-8px);
  border-color: #06b6d4;
  box-shadow: 0 20px 40px rgba(6, 182, 212, 0.2);
}

.member-card:hover .card-glow {
  opacity: 1;
}

.card-content {
  position: relative;
  z-index: 1;
  text-align: center;
}

.member-avatar {
  position: relative;
  width: 100px;
  height: 100px;
  margin: 0 auto 1.5rem;
}

.avatar-ring {
  position: absolute;
  inset: -4px;
  border-radius: 50%;
  background: linear-gradient(135deg, #06b6d4, #3b82f6);
  animation: rotate 3s linear infinite;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

.avatar-text {
  position: absolute;
  inset: 4px;
  background: #0f172a;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  font-weight: 700;
  color: #06b6d4;
}

.member-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #f4f4f5;
}

.member-role {
  color: #06b6d4;
  font-size: 0.95rem;
  margin-bottom: 1.5rem;
}

.card-footer {
  padding-top: 1rem;
  border-top: 1px solid rgba(6, 182, 212, 0.2);
}

.view-profile {
  color: #06b6d4;
  font-size: 0.9rem;
  font-weight: 600;
  transition: all 0.3s ease;
}

.member-card:hover .view-profile {
  transform: translateX(4px);
  display: inline-block;
}

/* Profile View */
.profile-view {
  animation: slideIn 0.5s ease;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.back-button {
  background: rgba(15, 23, 42, 0.6);
  border: 1px solid rgba(6, 182, 212, 0.3);
  color: #e4e4e7;
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
  font-size: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 2rem;
  transition: all 0.3s ease;
}

.back-button:hover {
  background: rgba(6, 182, 212, 0.1);
  border-color: #06b6d4;
  transform: translateX(-4px);
}

.back-arrow {
  font-size: 1.25rem;
  transition: transform 0.3s ease;
}

.back-button:hover .back-arrow {
  transform: translateX(-4px);
}

.profile-container {
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(6, 182, 212, 0.2);
  border-radius: 1.5rem;
  padding: 3rem;
  backdrop-filter: blur(10px);
}

.profile-header {
  display: flex;
  gap: 3rem;
  margin-bottom: 3rem;
  padding-bottom: 3rem;
  border-bottom: 1px solid rgba(6, 182, 212, 0.2);
  align-items: center;
}

.profile-avatar-large {
  position: relative;
  width: 150px;
  height: 150px;
  flex-shrink: 0;
}

.avatar-ring-large {
  position: absolute;
  inset: -6px;
  border-radius: 50%;
  background: linear-gradient(135deg, #06b6d4, #3b82f6, #8b5cf6);
  animation: rotate 4s linear infinite;
}

.avatar-text-large {
  position: absolute;
  inset: 6px;
  background: #0f172a;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
  font-weight: 700;
  color: #06b6d4;
}

.profile-intro {
  flex: 1;
}

.profile-name {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  color: #f4f4f5;
}

.profile-role {
  font-size: 1.25rem;
  color: #06b6d4;
  margin-bottom: 1rem;
}

.profile-meta {
  display: flex;
  gap: 1rem;
  align-items: center;
  color: #a1a1aa;
  font-size: 0.95rem;
}

.meta-label {
  font-weight: 600;
  margin-right: 0.5rem;
}

.meta-value {
  color: #e4e4e7;
}

.meta-divider {
  color: rgba(6, 182, 212, 0.3);
}

/* Profile Grid */
.profile-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.profile-section {
  background: rgba(10, 14, 39, 0.4);
  border: 1px solid rgba(6, 182, 212, 0.2);
  border-radius: 1rem;
  padding: 2rem;
  transition: all 0.3s ease;
}

.profile-section:hover {
  border-color: #06b6d4;
  box-shadow: 0 10px 30px rgba(6, 182, 212, 0.1);
}

.section-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid rgba(6, 182, 212, 0.2);
}

.section-icon {
  font-size: 1.5rem;
}

.section-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: #f4f4f5;
}

.section-content {
  color: #d4d4d8;
  line-height: 1.6;
}

/* Studies */
.study-item {
  padding: 1rem;
  background: rgba(6, 182, 212, 0.05);
  border-left: 3px solid #06b6d4;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}

.study-item:last-child {
  margin-bottom: 0;
}

.study-degree {
  font-weight: 700;
  color: #f4f4f5;
  margin-bottom: 0.25rem;
}

.study-institution {
  color: #06b6d4;
  font-size: 0.95rem;
  margin-bottom: 0.25rem;
}

.study-year {
  color: #a1a1aa;
  font-size: 0.85rem;
}

/* Skills */
.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.skill-tag {
  background: rgba(6, 182, 212, 0.1);
  border: 1px solid rgba(6, 182, 212, 0.3);
  color: #06b6d4;
  padding: 0.5rem 1rem;
  border-radius: 2rem;
  font-size: 0.9rem;
  font-weight: 600;
  transition: all 0.3s ease;
}

.skill-tag:hover {
  background: rgba(6, 182, 212, 0.2);
  border-color: #06b6d4;
  transform: translateY(-2px);
}

/* Bio */
.bio-text {
  font-size: 1rem;
  line-height: 1.7;
}

/* Social Links */
.social-links {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1rem;
  background: rgba(6, 182, 212, 0.05);
  border: 1px solid rgba(6, 182, 212, 0.2);
  border-radius: 0.5rem;
  color: #e4e4e7;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-link:hover {
  background: rgba(6, 182, 212, 0.1);
  border-color: #06b6d4;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(6, 182, 212, 0.2);
}

.social-icon {
  font-size: 1.25rem;
}

.social-name {
  font-size: 0.9rem;
  font-weight: 600;
}

/* Footer */
.footer {
  position: relative;
  z-index: 10;
  text-align: center;
  padding: 2rem;
  margin-top: 4rem;
  border-top: 1px solid rgba(6, 182, 212, 0.2);
  color: #71717a;
  font-size: 0.9rem;
}

/* Transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.4s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(20px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-20px);
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1rem;
  }

  .team-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .profile-container {
    padding: 2rem 1.5rem;
  }

  .profile-header {
    flex-direction: column;
    text-align: center;
    gap: 2rem;
  }

  .profile-name {
    font-size: 2rem;
  }

  .profile-grid {
    grid-template-columns: 1fr;
  }

  .main-content {
    padding: 1rem;
  }
}

@media (max-width: 480px) {
  .header {
    padding: 1rem;
  }

  .logo {
    font-size: 1.25rem;
  }

  .hero-title {
    font-size: 2rem;
  }

  .profile-avatar-large {
    width: 120px;
    height: 120px;
  }

  .avatar-text-large {
    font-size: 2.5rem;
  }
}
</style>