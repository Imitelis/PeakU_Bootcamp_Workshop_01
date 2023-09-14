<template>
    <div class="search-bar navbar navbar-expand navbar-primary" :style="getSearchBarWidth" :class="{ 'stickyBar': sticky }">
        <div class="navbar-search" id="search">
            <input type="text" class="search-input py-2" placeholder="Search by role, salary, location, or company">
            <span class="search-icon"><svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" class="bi bi-search mb-0" viewBox="0 0 16 16"> <path :d="svgdSearch"/></svg></span>
        </div>
        <nav class="navbar-items" :style="getSearchWidth">
        <ul class="navbar-nav">
          <li class="nav-item"><button class="nav-button btn btn-outline-light px-2" @click="showAreas" :class="{ 'active': isAreaPopup }"><span class="px-2">Area</span><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" class="bi bi-caret mb-0" viewBox="0 0 16 16"> <path :d="svgdOptions"/></svg></button></li>
          <li class="nav-item"><button class="nav-button btn btn-outline-light px-2" @click="showRoles" :class="{ 'active': isRolePopup }"><span class="px-2">Role</span><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" class="bi bi-caret mb-0" viewBox="0 0 16 16"> <path :d="svgdOptions"/></svg></button></li>
          <li class="nav-item"><button class="nav-button btn btn-outline-light px-2" @click="showSalaries" :class="{ 'active': isSalaryPopup }"><span class="px-2">Salary</span><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" class="bi bi-caret mb-0" viewBox="0 0 16 16"> <path :d="svgdOptions"/></svg></button></li>
          <li class="nav-item"><button class="nav-button btn btn-outline-light px-2" @click="showLocations" :class="{ 'active': isLocationPopup }"><span class="px-2">Location</span><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" class="bi bi-caret mb-0" viewBox="0 0 16 16"> <path :d="svgdOptions"/></svg></button></li>
        </ul>
        </nav>
        <div v-if="isAreaPopup" class="darkened-background">
        <div class="popup-search">
          <div class="popup-header">
            <img v-bind:src="popupBackground">
          </div>
          <span class="popup-title mx-2">Choose a work area <span @click="hideAreas" class="popup-close"><svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" fill="currentColor" class="bi bi-times" viewBox="0 0 16 16"> <path :d="svgdTimes"/></svg></span></span>
          <div class="popup-content">
            <label><input type="checkbox" class="input-checkbox">Accounting & Finance</label>
            <label><input type="checkbox" class="input-checkbox">Customer service</label>
            <label><input type="checkbox" class="input-checkbox">Design</label>
            <label><input type="checkbox" class="input-checkbox">International trade</label>
            <label><input type="checkbox" class="input-checkbox">Logistics and Transport</label>
            <label><input type="checkbox" class="input-checkbox">Marketing</label>
            <label><input type="checkbox" class="input-checkbox">Other</label>
            <label><input type="checkbox" class="input-checkbox">Recruiting</label>
            <label><input type="checkbox" class="input-checkbox">Marketing</label>
            <label><input type="checkbox" class="input-checkbox">Sales</label>
            <label><input type="checkbox" class="input-checkbox">Technology</label>
          </div>
          <div class="popup-footer">
            <button class="btn btn-outline-secondary btn-block text-gray" @click="hideAreas">Close</button>
            <button class="btn btn-block text-white apply-button" @click="hideAreas">Apply</button>
          </div>
        </div>
      </div>
      <div v-if="isRolePopup" class="darkened-background">
        <div class="popup-search">
          <div class="popup-header">
            <img v-bind:src="popupBackground">
          </div>
          <span class="popup-title mx-2">Choose one or more roles <span @click="hideRoles" class="popup-close"><svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" fill="currentColor" class="bi bi-times" viewBox="0 0 16 16"> <path :d="svgdTimes"/></svg></span></span>
          <div class="popup-content">
            <select class="select-options" required>
              <option disabled="" selected="" value>All roles</option>
              <option>Accounting & Finance</option>
              <option>Customer Service</option>
              <option>Design</option>
              <option>International trade</option>
              <option>Logistics and Transport</option>
              <option>Marketing</option>
              <option>Recruiting</option>
              <option>Sales</option>
              <option>Technology</option>
            </select>
          </div>
          <div class="popup-footer">
            <button class="btn btn-outline-secondary btn-block text-gray" @click="hideRoles">Close</button>
            <button class="btn btn-block text-white apply-button" @click="hideRoles">Apply</button>
          </div>
        </div>
      </div>
      <div v-if="isSalaryPopup" class="darkened-background">
        <div class="popup-search">
          <div class="popup-header">
            <img v-bind:src="popupBackground">
          </div>
          <span class="popup-title mx-2">Salary range <span @click="hideSalaries" class="popup-close"><svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" fill="currentColor" class="bi bi-times" viewBox="0 0 16 16"> <path :d="svgdTimes"/></svg></span></span>
          <div class="popup-content">
            <select class="select-options" required>
              <option disabled="" selected="" value>Currency</option>
              <option>US Dollar</option>
              <option>Colombian Peso</option>
              <option>Mexican Peso</option>
              <option>Argentinean Peso</option>
              <option>Chilean Peso</option>
              <option>Real Brasileiro</option>
              <option>Euro</option>
            </select>
            <div class="salary-options">
              <input class="salary-input" type="number" min="0" max="100000" placeholder="Min">
              <input class="salary-input" type="number" min="0" max="100000" placeholder="Max">
            </div>
          </div>
          <div class="popup-footer">
            <button class="btn btn-outline-secondary btn-block text-gray" @click="hideSalaries">Close</button>
            <button class="btn btn-block text-white apply-button" @click="hideSalaries">Apply</button>
          </div>
        </div>
      </div>
      <div v-if="isLocationPopup" class="darkened-background">
        <div class="popup-search">
          <div class="popup-header">
            <img v-bind:src="popupBackground">
          </div>
          <span class="popup-title mx-2">Choose a location <span @click="hideLocations" class="popup-close"><svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" fill="currentColor" class="bi bi-times" viewBox="0 0 16 16"> <path :d="svgdTimes"/></svg></span></span>
          <div class="popup-content">
            <select class="select-options" required>
              <option disabled="" selected="" value>Unselected</option>
              <option>Bogotá</option>
              <option>Medellín</option>
              <option>Ciudad de México</option>
              <option>Buenos Aires</option>
              <option>Santiago</option>
              <option>Rio de Janeiro</option>
              <option>New York</option>
            </select>
          </div>
          <div class="popup-footer">
            <button class="btn btn-outline-secondary btn-block text-gray" @click="hideLocations">Close</button>
            <button class="btn btn-block text-white apply-button" @click="hideLocations">Apply</button>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'SearchBar',
  props: ['expanded', 'sticky'],
  data() {
    return {
      popupBackground: require('../assets/images/PopupBackground.png'),
      svgdSearch: "M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z",
      svgdOptions: "M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z",
      svgdTimes: "M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z",
      isAreaPopup: false,
      isRolePopup: false,
      isSalaryPopup: false,
      isLocationPopup: false,
    }
  },
  computed: {
    getSearchBarWidth() {
      const collapsedWidth = 'calc(100vw - 215px)';
      const expandedWidth = 'calc(100vw - 100px)';
      const expandedLeft = '90px';
      const collapsedLeft = '205px';
      return this.expanded ? { width: collapsedWidth, left: collapsedLeft } : { width: expandedWidth, left: expandedLeft };
    },
    getSearchWidth() {
      const expandedLeft = '28vw';
      const collapsedLeft = '18vw';
      return this.expanded ? { left: collapsedLeft } : { left: expandedLeft };
    }
  },
  methods: {
    showAreas() {
      this.isAreaPopup = true;
      this.isRolePopup = false;
      this.isSalaryPopup = false;
      this.isLocationPopup = false;
      document.body.style.overflow = 'hidden';
    },
    hideAreas() {
      this.isAreaPopup = false;
      document.body.style.overflow = 'auto';
    },
    showRoles() {
      this.isAreaPopup = false;
      this.isRolePopup = true;
      this.isSalaryPopup = false;
      this.isLocationPopup = false;
      document.body.style.overflow = 'hidden';
    },
    hideRoles() {
      this.isRolePopup = false;
      document.body.style.overflow = 'auto';
    },
    showSalaries() {
      this.isAreaPopup = false;
      this.isRolePopup = false;
      this.isSalaryPopup = true;
      this.isLocationPopup = false;
      document.body.style.overflow = 'hidden';
    },
    hideSalaries() {
      this.isSalaryPopup = false;
      document.body.style.overflow = 'auto';
    },
    showLocations() {
      this.isAreaPopup = false;
      this.isRolePopup = false;
      this.isSalaryPopup = false;
      this.isLocationPopup = true;
      document.body.style.overflow = 'hidden';
    },
    hideLocations() {
      this.isLocationPopup = false;
      document.body.style.overflow = 'auto';
    },
  }
}
</script>

<style scoped>
.search-bar {
  position: relative;
  height: 74px;
  top: -50px;
  right: 0px;
  z-index: 1;
  background-image: url("@/assets/images/SearchBackground.png");
  background-size: cover;
  background-position: center;
  padding-left: 16px;
  padding-right: 16px;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-between;
  overflow: hidden;
  white-space: nowrap;
}

.search-bar.stickyBar {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.search-input {
  width: 480px;
  height: 38px;
  padding-right: 4px;
  padding-left: 42px;
  border-radius: 2.5px;
  margin-left: 8px;
  border: 0.5px solid rgba(255, 255, 255, 0.6);
}

.search-input::placeholder {
  font-size: 16px;
  font-weight: lighter;
}

.search-icon {
  position: relative;
  left: -470px;
  margin-top: 2px;
  z-index: 1;
}

.search-input:focus {
  outline: none;
  border-radius: 2.5px;
  border: 2px solid black;
}

.navbar-items {
  display: flex;
  flex-direction: row;
}

.nav-item {
  white-space: nowrap;
  display: inline-block;
}

.nav-button {
  margin-left: 6px;
  border-radius: 15px !important;
  padding-top: 2px;
  padding-bottom: 2px;
  font-size: 12x;
  color: white;
}

.popup-search {
  background-color: white;
  color: white;
  position: relative;
  display: flex;
  align-items: center;
  flex-direction: column;
  top: 20vh;
  left: 35vw;
  right: 35vw;
  z-index: 1;
  border: 1px solid rgba(0, 0, 0, 0.6);
  border-radius: 5px;
  width: 498px;
  overflow: hidden;
}

.popup-header {
  position: relative;
  display: block;
  top: 0px;
  left: 0px;
  width: 100%;
  z-index: -2;
}

.popup-title {
  font-size: 20px;
  font-weight: bold;
  position: relative;
  z-index: 2;
  top: -55px;
  right: -35px
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
  text-align: left;
  color: black;
  width: 100%;
  padding-left: 16px;
  padding-right: 16px;
  padding-top: 0px;
  padding-bottom: 16px;
  margin-top: -16px;
  margin-bottom: 12px;
  margin-left: 16px;
  margin-right: 16px;
  border-bottom: 1px solid #ccc;
  line-height: 1.3;
}

.apply-button {
  background-color: dodgerblue;
}

.apply-button:hover {
  background-color: steelblue;
}

.input-checkbox {
  margin-right: 6px;
}

.select-options {
  background-color: whitesmoke;
  color: black;
  border-radius: 5px;
  border: 1px solid #ccc;
  padding: 8px;
  height: 35px;
  width: 100%;
}

.salary-options {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin-top: 16px;
  gap: 24px;
}

.salary-input {
  background-color: whitesmoke;
  color: black;
  border-radius: 5px;
  border: 1px solid #ccc;
  padding: 8px;
  width: 220px;
}

.salary-input:focus {
  border-color: lightblue;
}

.popup-footer {
  margin-bottom: 12px;
  align-items: center;
}

.popup-footer button {
  margin-left: 12px;
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
  overflow: hidden;
}

@media (max-width: 1080px) {
  .search-bar {
    height: 100px;
    display: flex;
    flex-direction: column;
  }

  .navbar-nav {
    position: fixed;
    left: 24vw;
  }

  .navbar-items {
    margin-left: 60px;
    margin-top: 50px;
  }
}

</style>