<template>
    <div class="navigation-bar navbar navbar-expand-md navbar-light bg-light">
      <div class="navbar-brand" id="logo">
        <a href="/"><img src="https://peaku.co/img/logo-blue.png"></a>
      </div>
      <nav id="navbar">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item"><a class="nav-link" href="/jobs" @mouseenter="closeProfessionals(); closeBusiness(); closeUser()">Jobs</a></li>
          <li class="nav-item"><a class="nav-link" href="/bootcamp-fullstack" @mouseenter="closeProfessionals(); closeBusiness(); closeUser()">Bootcamp</a></li>
          <li class="nav-item"><a class="nav-link" href="/about-us" @mouseenter="closeProfessionals(); closeBusiness(); closeUser()">About Us</a></li>
          <li class="nav-item"><a class="nav-link" :class="{ 'active': isProfessionalsOpen }" href="/" @mouseenter="openProfessionals">For professionals <svg xmlns="http://www.w3.org/2000/svg" width="9" height="9" fill="currentColor" class="bi bi-caret mb-2" viewBox="0 0 16 16"> <path :d="svgdOptions"/></svg></a></li>
          <div @mouseleave="closeProfessionals">
            <div v-if="isProfessionalsOpen" class="professionals-options">
              <a class="option" href="/professionals">Home</a>
              <a class="option" href="/jobs">Jobs</a>
              <a class="option" href="/jobs">Courses and challenges</a>
              <a class="option" href="/jobs">Questions</a>
              <a class="option" href="/teachers">Teachers</a>
              <a class="option" href="/bootcamp-fullstack">Bootcamp</a>
            </div>
          </div>
          <li class="nav-item"><a class="nav-link" :class="{ 'active': isBusinessOpen }" href="/" @mouseenter="openBusiness">For business <svg xmlns="http://www.w3.org/2000/svg" width="9" height="9" fill="currentColor" class="bi bi-caret mb-2" viewBox="0 0 16 16"> <path :d="svgdOptions"/></svg></a></li>
          <div @mouseleave="closeBusiness">
            <div v-if="isBusinessOpen" class="business-options">
              <a class="option" href="/business">Home</a>
              <a class="option" href="/jobs">Post job</a>
              <a class="option" href="/jobs">Our process</a>
              <a class="option" href="/business">Pricing</a>
              <a class="option" href="/business">Assessments</a>
              <a class="option" href="/business">Payroll</a>
              <a class="option" href="/business">Blog</a>
              <a class="option" href="/business">Sales</a>
              <a class="option" href="/business">Salary calculator</a>
            </div>
          </div>
          <li class="nav-item"><button class="nav-link btn btn-sm btn-light my-1 mx-3" id="languages-button" @click="showLanguages" @mouseenter="closeProfessionals(); closeBusiness(); closeUser()"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-globe mx-1 my-0" viewBox="0 0 16 16"> <path :d="svgdGlobe"/></svg> English</button></li>
          <li class="nav-item"><button class="nav-link btn" data-bs-toggle="collapse" data-bs-target="#lateralMenu" @click="showNotifications" @mouseenter="closeProfessionals(); closeBusiness(); closeUser()"><span id="notification-icon"><span class="notification-status bg-danger text-white position-absolute">4</span><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-bell" viewBox="0 0 16 16"><path :d="svgdBell"/></svg></span></button></li>
          <li class="nav-item"><button class="nav-link btn d-flex" id="user-button" title="David Sensei" @click="openUser"><span id="user-image" class="bg-black rounded-circle px-1 py-0" ><svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="white" class="bi bi-user" viewBox="0 0 16 16"><path :d="svgdUser"/></svg></span><span id="user-info" class="user-details"><span>David</span><span><svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" fill="currentColor" class="bi bi-gem" viewBox="0 0 16 16"><path :d="svgdGem"/></svg> 999</span></span></button></li>
          <div @mouseleave="closeUser">
            <div v-if="isUserOpen" class="user-options">
              <a class="option" href="/reward">Redeem (999) <span class="mx-2"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-gem" viewBox="0 0 16 16"> <path :d="svgdGem"/></svg></span></a>
              <a class="option" href="/cv">Your CV</a>
              <a class="option" href="/settings">Settings</a>
              <a class="option" href="/settings">Change password</a>
              <a class="option" href="/jobs">Sign Out</a>            
            </div>
          </div>
        </ul>
      </nav>
      <div v-if="isLanguagesPopup" class="darkened-background">
        <div class="popup-languages">
          <div class="popup-header">
            <img v-bind:src="popupBackground">
            <span class="popup-title mx-2">Choose a language <span @click="hideLanguages" class="popup-close"><svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" fill="currentColor" class="bi bi-times" viewBox="0 0 16 16"> <path :d="svgdTimes"/></svg></span></span>
          </div>
          <div class="popup-content">
            <button class="btn btn-outline-secondary btn-block text-gray">Spanish</button>
            <button class="btn btn-outline-secondary btn-block text-gray" autofocus>English</button>
            <button class="btn btn-outline-secondary btn-block text-gray">Portuguese</button>
          </div>
        </div>
      </div>
      <div v-if="isNotificationBar" class="darkened-notification" :class="{ active: isNotificationBar }">
        <div class="notification-bar bg-light">
          <div class="notification-header">
            <button @click="hideNotifications" type="button" class="btn-close btn-sm"></button>
            <h3 class="notification-title">Notifications</h3>
          </div>
          <a class="notification-refresh" href="/">Refresh</a>
          <div class="notification">
            <span class="notification-form mt-20"><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="dodgerblue" class="bi bi-gem" viewBox="0 0 16 16"> <path :d="svgdGem"/></svg></span><span id="notification-text"><span class="text-black">You have earned 15 for complete practice test!</span><span class="text-lightgray">2 days ago</span></span>
          </div>
          <div class="notification">
            <span class="notification-form mt-20"><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="dodgerblue" class="bi bi-gamepad mb-1" viewBox="0 0 16 16"> <path :d="svgdGamepad01"/> <path :d="svgdGamepad02"/></svg></span><span id="notification-text"><span class="text-black">You have completed the command line basics exercise</span><span class="text-lightgray">2 days ago</span></span>
          </div>
          <div class="notification">
            <span class="notification-form mt-20"><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="dodgerblue" class="bi bi-gem" viewBox="0 0 16 16"> <path :d="svgdGem"/></svg></span><span id="notification-text"><span class="text-black">You have earned 15 for complete practice test!</span><span class="text-lightgray">3 days ago</span></span>
          </div>
          <div class="notification">
            <span class="notification-form mt-20"><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="dodgerblue" class="bi bi-gamepad mb-1" viewBox="0 0 16 16"> <path :d="svgdGamepad01"/> <path :d="svgdGamepad02"/></svg></span><span id="notification-text"><span class="text-black">You have completed the logical operators exercise</span><span class="text-lightgray">3 days ago</span></span>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'NavigationBar',
  props: {
    
  },
  data() {
    return {
      isHidden: false,
        isProfessionalsOpen: false,
        isBusinessOpen: false,
        isUserOpen: false,
        svgdOptions: "M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z",
        svgdGlobe: "M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8zm7.5-6.923c-.67.204-1.335.82-1.887 1.855A7.97 7.97 0 0 0 5.145 4H7.5V1.077zM4.09 4a9.267 9.267 0 0 1 .64-1.539 6.7 6.7 0 0 1 .597-.933A7.025 7.025 0 0 0 2.255 4H4.09zm-.582 3.5c.03-.877.138-1.718.312-2.5H1.674a6.958 6.958 0 0 0-.656 2.5h2.49zM4.847 5a12.5 12.5 0 0 0-.338 2.5H7.5V5H4.847zM8.5 5v2.5h2.99a12.495 12.495 0 0 0-.337-2.5H8.5zM4.51 8.5a12.5 12.5 0 0 0 .337 2.5H7.5V8.5H4.51zm3.99 0V11h2.653c.187-.765.306-1.608.338-2.5H8.5zM5.145 12c.138.386.295.744.468 1.068.552 1.035 1.218 1.65 1.887 1.855V12H5.145zm.182 2.472a6.696 6.696 0 0 1-.597-.933A9.268 9.268 0 0 1 4.09 12H2.255a7.024 7.024 0 0 0 3.072 2.472zM3.82 11a13.652 13.652 0 0 1-.312-2.5h-2.49c.062.89.291 1.733.656 2.5H3.82zm6.853 3.472A7.024 7.024 0 0 0 13.745 12H11.91a9.27 9.27 0 0 1-.64 1.539 6.688 6.688 0 0 1-.597.933zM8.5 12v2.923c.67-.204 1.335-.82 1.887-1.855.173-.324.33-.682.468-1.068H8.5zm3.68-1h2.146c.365-.767.594-1.61.656-2.5h-2.49a13.65 13.65 0 0 1-.312 2.5zm2.802-3.5a6.959 6.959 0 0 0-.656-2.5H12.18c.174.782.282 1.623.312 2.5h2.49zM11.27 2.461c.247.464.462.98.64 1.539h1.835a7.024 7.024 0 0 0-3.072-2.472c.218.284.418.598.597.933zM10.855 4a7.966 7.966 0 0 0-.468-1.068C9.835 1.897 9.17 1.282 8.5 1.077V4h2.355z",
        svgdBell: "M8 16a2 2 0 0 0 2-2H6a2 2 0 0 0 2 2zM8 1.918l-.797.161A4.002 4.002 0 0 0 4 6c0 .628-.134 2.197-.459 3.742-.16.767-.376 1.566-.663 2.258h10.244c-.287-.692-.502-1.49-.663-2.258C12.134 8.197 12 6.628 12 6a4.002 4.002 0 0 0-3.203-3.92L8 1.917zM14.22 12c.223.447.481.801.78 1H1c.299-.199.557-.553.78-1C2.68 10.2 3 6.88 3 6c0-2.42 1.72-4.44 4.005-4.901a1 1 0 1 1 1.99 0A5.002 5.002 0 0 1 13 6c0 .88.32 4.2 1.22 6z",
        svgdGem: "M3.1.7a.5.5 0 0 1 .4-.2h9a.5.5 0 0 1 .4.2l2.976 3.974c.149.185.156.45.01.644L8.4 15.3a.5.5 0 0 1-.8 0L.1 5.3a.5.5 0 0 1 0-.6l3-4zm11.386 3.785-1.806-2.41-.776 2.413 2.582-.003zm-3.633.004.961-2.989H4.186l.963 2.995 5.704-.006zM5.47 5.495 8 13.366l2.532-7.876-5.062.005zm-1.371-.999-.78-2.422-1.818 2.425 2.598-.003zM1.499 5.5l5.113 6.817-2.192-6.82L1.5 5.5zm7.889 6.817 5.123-6.83-2.928.002-2.195 6.828z",
        svgdTimes: "M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z",
        svgdUser: "M8 8a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm2-3a2 2 0 1 1-4 0 2 2 0 0 1 4 0zm4 8c0 1-1 1-1 1H3s-1 0-1-1 1-4 6-4 6 3 6 4zm-1-.004c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10c-2.29 0-3.516.68-4.168 1.332-.678.678-.83 1.418-.832 1.664h10z",
        svgdGamepad01: "M11.5 6.027a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0zm-1.5 1.5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1zm2.5-.5a.5.5 0 1 1-1 0 .5.5 0 0 1 1 0zm-1.5 1.5a.5.5 0 1 0 0-1 .5.5 0 0 0 0 1zm-6.5-3h1v1h1v1h-1v1h-1v-1h-1v-1h1v-1z",
        svgdGamepad02: "M3.051 3.26a.5.5 0 0 1 .354-.613l1.932-.518a.5.5 0 0 1 .62.39c.655-.079 1.35-.117 2.043-.117.72 0 1.443.041 2.12.126a.5.5 0 0 1 .622-.399l1.932.518a.5.5 0 0 1 .306.729c.14.09.266.19.373.297.408.408.78 1.05 1.095 1.772.32.733.599 1.591.805 2.466.206.875.34 1.78.364 2.606.024.816-.059 1.602-.328 2.21a1.42 1.42 0 0 1-1.445.83c-.636-.067-1.115-.394-1.513-.773-.245-.232-.496-.526-.739-.808-.126-.148-.25-.292-.368-.423-.728-.804-1.597-1.527-3.224-1.527-1.627 0-2.496.723-3.224 1.527-.119.131-.242.275-.368.423-.243.282-.494.575-.739.808-.398.38-.877.706-1.513.773a1.42 1.42 0 0 1-1.445-.83c-.27-.608-.352-1.395-.329-2.21.024-.826.16-1.73.365-2.606.206-.875.486-1.733.805-2.466.315-.722.687-1.364 1.094-1.772a2.34 2.34 0 0 1 .433-.335.504.504 0 0 1-.028-.079zm2.036.412c-.877.185-1.469.443-1.733.708-.276.276-.587.783-.885 1.465a13.748 13.748 0 0 0-.748 2.295 12.351 12.351 0 0 0-.339 2.406c-.022.755.062 1.368.243 1.776a.42.42 0 0 0 .426.24c.327-.034.61-.199.929-.502.212-.202.4-.423.615-.674.133-.156.276-.323.44-.504C4.861 9.969 5.978 9.027 8 9.027s3.139.942 3.965 1.855c.164.181.307.348.44.504.214.251.403.472.615.674.318.303.601.468.929.503a.42.42 0 0 0 .426-.241c.18-.408.265-1.02.243-1.776a12.354 12.354 0 0 0-.339-2.406 13.753 13.753 0 0 0-.748-2.295c-.298-.682-.61-1.19-.885-1.465-.264-.265-.856-.523-1.733-.708-.85-.179-1.877-.27-2.913-.27-1.036 0-2.063.091-2.913.27z",
        isLanguagesPopup: false,
        isNotificationBar: false,
        popupBackground: require('../assets/images/PopupBackground.png')
    };
  },
  computed: {
    observerOptions() {
      return {
        root: null,
        rootMargin: '0px',
        threshold: 0,
      };
    },
  },
  methods: {
    openProfessionals() {
      this.isProfessionalsOpen = true;
      this.isBusinessOpen = false;
      this.isUserOpen = false;
    },
    closeProfessionals() {
      this.isProfessionalsOpen = false;
    },
    openBusiness() {
      this.isBusinessOpen = true;
      this.isProfessionalsOpen = false;
      this.isUserOpen = false;
    },
    closeBusiness() {
      this.isBusinessOpen = false;
    },
    openUser() {
      this.isUserOpen = true;
      this.isProfessionalsOpen = false;
      this.isBusinessOpen = false;
    },
    closeUser() {
      this.isUserOpen = false;
    },
    showLanguages() {
      this.isLanguagesPopup = true;
      document.body.style.overflow = 'hidden';
    },
    hideLanguages() {
      this.isLanguagesPopup = false;
      document.body.style.overflow = 'auto';
    },
    showNotifications() {
      this.isNotificationBar = true;
      document.body.style.overflow = 'auto';
    },
    hideNotifications() {
      this.isNotificationBar = false;
      document.body.style.overflow = 'auto';
    }
  },
}
</script>

<style scoped>

.pushed-up {
  height: 0;
  overflow: hidden;
}
.navigation-bar {
  position: absolute;
  height: 70px;
  width: 100vw;
  top: 0px;
  left: 0px;
  border: 1px solid #ccc;
  z-index: 3;
}

#logo {
    padding: 5px;
}

#navbar {
  position: absolute;
  margin-top: 5px;
  right: 5px;
}

.navbar-nav {
  display: flex;
  flex-direction: row;
}

#navbar a {
  font-size: medium;
  text-decoration: none;
  color: gray;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  margin-right: 8px;
}

#navbar a.active,
#navbar a:hover {
    color: black;
}

.professionals-options, .business-options, .user-options {
  display: flex;
  flex-direction: column;
  background-color: white;
  position: absolute;
  border: 2px solid lightgrey;
  border-radius: 5px;
  margin-top: 50px;
  margin-bottom: 0px;
  z-index: 2;
}

.professionals-options {
  width: 245px;
  padding: 5px;
  top: -18px;
  right: 32vw;
}
.business-options {
  width: 195px;
  padding: 5px;
  top: -18px;
  right: 22vw;
}

.user-options {
  width: 185px;
  padding-top: 5px;
  padding-bottom: 5px;
  top: -12px;
  right: 5px;
}

.professionals-options a, .business-options a, .user-options a {
  color: black;
  display: flex;
  text-decoration: none;
  align-items: left;
  text-align: left;
  padding-left: 22px;
  padding-top: 4px;
  padding-bottom: 4px;
  margin-bottom: 2px;
  border-radius: 2.5px;
  border: 1px solid white;
}

.professionals-options a:hover, .business-options a:hover, .user-options a:hover {
  background-color:	rgba(224,255,255, 0.6);
  border: 1px solid rgba(211, 211, 211, 0.4);
}

#languages-button {
  background-color: whitesmoke;
  display: flex;
  border: 2px;
  font-size: 14px;
  color: gray;
  margin-left: 15px;
  border: 2px solid rgba(211, 211, 211, 0.4);
  border-radius: 5px;
  padding-top: 4px;
  padding-bottom: 2px;
  padding-left: 15px;
  padding-right: 15px;
}

#languages-icon {
  right: 4px;
}

#languages-button:hover {
    color: black;
}

#notification-icon {
  margin-left: 4px;
  padding-right: 8px;
  padding-left: 10px;
  padding-top: 6px;
  padding-bottom: 6px;
  position: relative;
  border: 2px solid transparent;
}

#notification-icon:hover {
  outline: 2px solid rgba(211, 211, 211, 0.4);
  border-radius: 2.5px;
  background-color: rgba(224, 255, 255, 0.6);
}

#notification-icon svg {
  box-sizing: content-box;
}

.notification-status {
  font-size: 12px;
  border-radius: 50%;
  width: 16px;
  height: 16px;
  top: -8px;
  right: 28px;
}

#user-button {
  margin-right: 2px;
  padding-right: 6px;
  padding-left: 2px;
  padding-top: 2px;
  padding-bottom: 2px;
  border: 2px solid transparent;
}

#user-button:hover, #user-button:active {
  outline: 2px solid rgba(211, 211, 211, 0.4);
  border-radius: 2.5px;
  background-color: rgba(224, 255, 255, 0.6);
}

.user-details {
  display: flex;
  flex-direction: column;
  color: gray;
  font-size: 9px;
  text-align: left;
  margin-left: 5px;
}

.popup-languages {
  background-color: white;
  color: white;
  position: fixed;
  display: flex;
  align-items: center;
  flex-direction: column;
  top: 25%;
  left: 30%;
  right: 30%;
  z-index: 1;
  border: 1px solid rgba(0, 0, 0, 0.6);
  border-radius: 5px;
  width: 498px;
  overflow: hidden; 
}

.popup-header {
  position: relative;
  display: block;
  overflow: hidden;
  top: 0px;
  left: 0px;
  width: 100%;
}

.popup-title {
  font-size: 20px;
  font-weight: bold;
  position: relative;
  z-index: 2;
  top: -55px;
  right: -65px
}

.popup-close {
  cursor: pointer;
  margin-left: 100px;
}

.popup-close:hover {
  color: rgba(255, 255, 255, 0.6)
}

.popup-content {
  display: flex;
  flex-direction: column;
  padding-bottom: 36px;
  gap: 10px;
  width: 100%;
  padding-left: 5px;
  padding-right: 5px;
}

.notification-bar {
  width: 320px;
  position: fixed;
  height: 100vh;
  right: 0px;
  overflow: visible;
  z-index: 2;
}

.notification-header {
  display: flex;
  flex-direction: row;
  margin: 15px;
  margin-bottom: 0px;
}

.notification-title {
 margin-left: 100px;
 font-weight: bold; 
}

.notification-refresh {
  text-decoration: none;
  font-size: 14px;
}

.notification-refresh:hover {
  text-decoration: underline;
}

#notification-text {
  display: flex;
  flex-direction: column;
  text-align: left;
  margin-left: 6px;
  margin-right: 40px;
  font-size: 13px;
  font-weight: lighter;
  line-height: 20px;
  letter-spacing: 0.5px;
  width: 240px;
}

.notification {
  display: flex;
  align-items: center;
  padding-top: 6px;
  padding-right: 0px;
  padding-left: 16px;
  margin-left: 1px;
  width: 317px;
  border-bottom: 1px solid #ccc;
  cursor: pointer;
}

.notification-form {
  margin: 5px;
  margin-right: 8px;
}

.darkened-notification {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  z-index: 1;
  overflow: auto;
}

.darkened-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(3px);
  z-index: 1;
}

@media (max-width: 980px) {
  .nav-item:nth-child(-n+8) {
    display: none;
  }

  .professionals-options, .business-options {
    display: none;
  }
}

@media (max-width: 740px) {
  .user-details {
    display: none;
  }
}
</style>