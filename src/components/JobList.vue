<template>
  <div class="job-list bg-light" :style="getJobListWidth">
    <div class="job-offers">
      <div v-for="jobOffer in jobOffers" :key="jobOffer.id">
        <JobOffer :jobOffer="jobOffer" />      
      </div>
    </div>
    <div class="footer">
      <img v-bind:src="footerImage">
      <div class="footer-content">
      <span class="footer-title text-white mx-2">Discover a new way to find a job!</span>
      <span class="footer-cols">
        <span class="footer-option">
          <div class="title-option">Top jobs</div>
          <a class="option" href="/jobs">Bootcamp Training Fullstack Cohort 9</a>
          <a class="option" href="/jobs">Fullstack Developer (.Net - Javascript-SQL)</a>
          <a class="option" href="/jobs">Nursing assistant</a>
          <a class="option" href="/jobs">Fullstack Developer (English B2)</a>
          <a class="option" href="/jobs">Technician in Pharmaceutical Services / Cali</a>
        </span>
        <span class="footer-option">
          <div class="title-option">Top job categories</div>
          <a class="option" href="/jobs">Fullstack</a>
          <a class="option" href="/jobs">Backend Dev</a>
          <a class="option" href="/jobs">Frontend Dev</a>
          <a class="option" href="/jobs">Customer Support - Other</a>
          <a class="option" href="/jobs">Sales Executive</a>
        </span>
        <span class="footer-option">
          <div class="title-option">Business</div>
          <a class="option" href="/jobs">Post job</a>
          <a class="option" href="/jobs">Pricing</a>
          <a class="option" href="/jobs">Our process</a>
          <a class="option" href="/jobs">Sales</a>
        </span>
        <span class="footer-option">
          <div class="title-option">Legal</div>
          <a class="option" href="/jobs">Terms and conditions</a>
          <a class="option" href="/jobs">Privacy policy</a>
        </span>
      </span>
      <span class="footer-contact">
        <span class="contact-option text-white mx-2">
          <a href="https://www.facebook.com/"><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="white" class="bi bi-facebook" viewBox="0 0 16 16"> <path :d="svgdFacebook"/></svg></a>
          <a href="https://www.instagram.com/"><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="white" class="bi bi-instagram" viewBox="0 0 16 16"> <path :d="svgdInstagram"/></svg></a>
          <a href="https://www.linkedin.com/"><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="white" class="bi bi-linkedin" viewBox="0 0 16 16"> <path :d="svgdLinkedIn"/></svg></a>
        </span>
        <br/>
        <span class="contact-title text-white mx-2">
          © 2023 PeakU Inc. All Rights Reserved.
        </span>
      </span>
      </div>
    </div>
  </div>
</template>

<script>
import JobOffer from './JobOffer.vue'

export default {
  name: 'JobList',
  components: {
    JobOffer
  },
  props: ['expanded'],
  data() {
    return {
      jobOffers: [
          { id: "10879", title: "Pharmaceutical Services Technician / Cairo", logo: "jobLogo04", skills: ["Office automation", "Text Writing", "Assertive Communication"], company: "OFFIMEDICAS S.A.S.", location: "In Office (Santiago de Cali)", salary: "$ 1.4M COP", vacancy: "50 Jobs", published: "about 3 hours ago", icons: { "Certifications": "📄", "End year's party": "🥳", "Training": "📄" } },
          { id: "10870", title: "Technician in Pharmaceutical Services / San Alberto", logo: "jobLogo04", skills: ["Office automation", "Text Writing", "Assertive Communication"], company: "OFFIMEDICAS S.A.S.", location: "In Office ()", salary: "$ 1.4M COP", vacancy: "50 Jobs", published: "about 19 hours ago", icons: { "Certifications": "📄", "End year's party": "🥳", "Training": "📄" } },
          { id: "10865", title: "Database Administrator", logo: "jobLogo05", skills: ["Git", "Apis", "C# .Net"], company: "Magnum Logistics Sas", location: "Antioquia", salary: "$ 0 COP", vacancy: "1 Job", published: "about 22 hours ago", icons: { "...": "..." } },
          { id: "10864", title: "UX/UI Designer", logo: "jobLogo05", skills: ["Ux/Ui", "Ux Research", "Ux Ui Design"], company: "Magnum Logistics Sas", location: "Antioquia", salary: "$ 0 COP", vacancy: "1 Job", published: "1 day ago", icons: { "...": "..." } },
          { id: "10863", title: "Disc tests", logo: "jobLogo01", skills: [], company: "PeakU Inc.", location: "Remote", salary: "$ 0 COP", vacancy: "1 Job", published: "about 22 hours ago", icons: {"English coaching": "🌐", "Remote job": "📍", "Flexible schedule": "⌚"} },
          { id: "10853", title: "Cloud Management Specialist", logo: "jobLogo02", skills: ["Cloud Computing", "Cloud", "Blue"], company: "Data Tools", location: "Bogotá", salary: "Confidential", vacancy: "1 Job", published: "1 day ago", icons: {"English coaching": "🌐", "Remote job": "📍", "Flexible schedule": "⌚"} },
          { id: "10844", title: "Sr .Net Developer", logo: "jobLogo03", skills: ["Conversational English", "Sql Server", ".Net"], company: "VICHARA TECHNOLOGIES", location: "Remote in Colombia", salary: "$ 7M - 9M COP", vacancy: "1 Job", published: "4 days ago", icons: {"Private health insurance": "❤️", "Flexible schedule": "⌚", "Remote job": "📍"} },
          { id: "10840", title: "Performance evaluation test 2023", logo: "jobLogo01", skills: ["Leadership", "Performance"], company: "PeakU Inc.", location: "Remote", salary: "$ 0 COP", vacancy: "1 Job", published: "4 days ago", icons: {"English coaching": "🌐", "Remote job": "📍", "Flexible schedule": "⌚"} },
          { id: "10683", title: "Receptionist", logo: "jobLogo05", skills: ["Excel", "Client Service", "Marketing Tools"], company: "Hotel Casa Kolping", location: "Bogotá", salary: "$ 1.2M COP", vacancy: "1 Job", published: "14 days ago", icons: { "...": "..." } },
      ],
      footerImage: require('../assets/images/FooterBackground.png'),
      svgdFacebook: "M16 8.049c0-4.446-3.582-8.05-8-8.05C3.58 0-.002 3.603-.002 8.05c0 4.017 2.926 7.347 6.75 7.951v-5.625h-2.03V8.05H6.75V6.275c0-2.017 1.195-3.131 3.022-3.131.876 0 1.791.157 1.791.157v1.98h-1.009c-.993 0-1.303.621-1.303 1.258v1.51h2.218l-.354 2.326H9.25V16c3.824-.604 6.75-3.934 6.75-7.951z",
      svgdInstagram: "M8 0C5.829 0 5.556.01 4.703.048 3.85.088 3.269.222 2.76.42a3.917 3.917 0 0 0-1.417.923A3.927 3.927 0 0 0 .42 2.76C.222 3.268.087 3.85.048 4.7.01 5.555 0 5.827 0 8.001c0 2.172.01 2.444.048 3.297.04.852.174 1.433.372 1.942.205.526.478.972.923 1.417.444.445.89.719 1.416.923.51.198 1.09.333 1.942.372C5.555 15.99 5.827 16 8 16s2.444-.01 3.298-.048c.851-.04 1.434-.174 1.943-.372a3.916 3.916 0 0 0 1.416-.923c.445-.445.718-.891.923-1.417.197-.509.332-1.09.372-1.942C15.99 10.445 16 10.173 16 8s-.01-2.445-.048-3.299c-.04-.851-.175-1.433-.372-1.941a3.926 3.926 0 0 0-.923-1.417A3.911 3.911 0 0 0 13.24.42c-.51-.198-1.092-.333-1.943-.372C10.443.01 10.172 0 7.998 0h.003zm-.717 1.442h.718c2.136 0 2.389.007 3.232.046.78.035 1.204.166 1.486.275.373.145.64.319.92.599.28.28.453.546.598.92.11.281.24.705.275 1.485.039.843.047 1.096.047 3.231s-.008 2.389-.047 3.232c-.035.78-.166 1.203-.275 1.485a2.47 2.47 0 0 1-.599.919c-.28.28-.546.453-.92.598-.28.11-.704.24-1.485.276-.843.038-1.096.047-3.232.047s-2.39-.009-3.233-.047c-.78-.036-1.203-.166-1.485-.276a2.478 2.478 0 0 1-.92-.598 2.48 2.48 0 0 1-.6-.92c-.109-.281-.24-.705-.275-1.485-.038-.843-.046-1.096-.046-3.233 0-2.136.008-2.388.046-3.231.036-.78.166-1.204.276-1.486.145-.373.319-.64.599-.92.28-.28.546-.453.92-.598.282-.11.705-.24 1.485-.276.738-.034 1.024-.044 2.515-.045v.002zm4.988 1.328a.96.96 0 1 0 0 1.92.96.96 0 0 0 0-1.92zm-4.27 1.122a4.109 4.109 0 1 0 0 8.217 4.109 4.109 0 0 0 0-8.217zm0 1.441a2.667 2.667 0 1 1 0 5.334 2.667 2.667 0 0 1 0-5.334z",
      svgdLinkedIn: "M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0 .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854V1.146zm4.943 12.248V6.169H2.542v7.225h2.401zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248-.015-.709-.52-1.248-1.342-1.248-.822 0-1.359.54-1.359 1.248 0 .694.521 1.248 1.327 1.248h.016zm4.908 8.212V9.359c0-.216.016-.432.08-.586.173-.431.568-.878 1.232-.878.869 0 1.216.662 1.216 1.634v3.865h2.401V9.25c0-2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016a5.54 5.54 0 0 1 .016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225h2.4z",
    }
  },
  computed: {
    getJobListWidth() {
      const collapsedWidth = '84vw';
      const expandedWidth = '93vw';
      return this.expanded ? { width: collapsedWidth } : { width: expandedWidth };
    },
  }
}
</script>

<style scoped>

.job-offers {
  margin-top: 44px;
  margin-bottom: 50px;
}

.job-list {
  position: absolute;
  margin-top: 118px;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.2);
  right: 0;
  top: 0px;
}

.job-list::before {
  content: '';
  position: absolute;
  top: -60px;
  left: 0;
  width: 100%;
  height: 8px;
  box-shadow: 0 8px 8px rgba(0, 0, 0, 0.2);
  z-index: 0;
}

.footer {
  position: relative;
  justify-content: center;
  align-items: center;
  width: 99%;
  height: 60vh;
  min-height: 400px;
  bottom: 0px;
  left: 0px;
}

.footer img {
  position: absolute;
  width: 100%;
  height: 60vh;
  min-height: 400px;
  bottom: 0px;
  left: 0px;
}

.footer-content {
  position: absolute;
  top: 40px;
  left: 0;
  right: 0;
  color: white;
}

.footer-title {
  font-size: 34px;
}

.footer-cols {
  display: flex;
  flex-direction: row;
  width: auto;
  text-align: center;
  gap: 30px;
  font-size: 28px;
  margin-top: 25px;
  margin-left: 30px;
}

.footer-option {
  flex: 1;
  display: flex;
  display: flex;
  flex-direction: column;
  font-size: 16px;
  text-align: left;
  max-width: 270px;
  overflow-wrap: break-word;
  word-break: break-word;
}

.footer-option .title-option {
  font-size: 18px;
  padding-bottom: 6px;
  font-weight: bold;
}

.footer-option a {
  color: white;
  text-decoration: none;
  font-size: 14px;
}
.contact-title {
  font-size: 14px;
}

.footer-contact {
  align-items: center;
}

.contact-option {
  display: inline-flex;
  align-items: center;
  gap: 16px;
}

@media (max-width: 740px) {
  .footer, .footer img {
    min-height: 600px;
  }
}

@media (max-width: 520px) {
  .footer, .footer img {
    min-height: 800px;
  }
}

</style>
