<template>
    <div class="job-offer">
      <div class="job-logo">
        <img class="job-img" :src="getLogoUrl(jobOffer.logo)">
      </div>
      <div class="job-details">
        <a class="job-title" :href="`/jobs/${jobOffer.id}`" >{{ jobOffer.title }}</a>
        <span class="skill-list" v-for="skill in jobOffer.skills" :key="skill">
          <span class="job-skill">{{ skill }}</span>
        </span>
        <br/>
        <div class="job-specifications">
          <span><svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" fill="currentColor" class="bi bi-building" viewBox="0 0 16 16"><path :d="svgdBuilding01"/><path :d="svgdBuilding02"/></svg> {{ jobOffer.company }}</span>
          <span><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-location" viewBox="0 0 512 512"><path :d="svgdLocation01"/><path :d="svgdLocation02"/></svg> {{ jobOffer.location }}</span>
          <span><svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" class="bi bi-money" viewBox="0 0 256 256"><path :d="svgdMoney"/></svg>  {{ jobOffer.salary }}</span>
          <span><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-user" viewBox="0 0 24 24"><path :d="svgdUsers"/></svg>  {{ jobOffer.vacancy }}</span>
          <span><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-calendar" viewBox="0 0 16 16"><path :d="svgdCalendar01"/><path :d="svgdCalendar02"/></svg>  {{ jobOffer.published }}</span>
          <span class="icon-list">
            <span v-for="(key, value) in jobOffer.icons" :key="value"><span class="icon-extra" v-bind:title="value">{{ key }}</span></span>
          </span>
        </div>
      </div>
    </div>
</template>

  <script>
  export default {
    name: 'JobOffer',
    props: {
      jobOffer: {
        type: Object,
        required: true,
      },
    },
    data() {
      return {
        jobLogo01: require('../assets/logos/JobLogo01.png'),
        jobLogo02: require('../assets/logos/JobLogo02.png'),
        jobLogo03: require('../assets/logos/JobLogo03.png'),
        jobLogo04: require('../assets/logos/JobLogo04.png'),
        jobLogo05: require('../assets/logos/JobLogo05.png'),
        svgdBuilding01: "M14.763.075A.5.5 0 0 1 15 .5v15a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5V14h-1v1.5a.5.5 0 0 1-.5.5h-9a.5.5 0 0 1-.5-.5V10a.5.5 0 0 1 .342-.474L6 7.64V4.5a.5.5 0 0 1 .276-.447l8-4a.5.5 0 0 1 .487.022zM6 8.694 1 10.36V15h5V8.694zM7 15h2v-1.5a.5.5 0 0 1 .5-.5h2a.5.5 0 0 1 .5.5V15h2V1.309l-7 3.5V15z",
        svgdBuilding02: "M2 11h1v1H2v-1zm2 0h1v1H4v-1zm-2 2h1v1H2v-1zm2 0h1v1H4v-1zm4-4h1v1H8V9zm2 0h1v1h-1V9zm-2 2h1v1H8v-1zm2 0h1v1h-1v-1zm2-2h1v1h-1V9zm0 2h1v1h-1v-1zM8 7h1v1H8V7zm2 0h1v1h-1V7zm2 0h1v1h-1V7zM8 5h1v1H8V5zm2 0h1v1h-1V5zm2 0h1v1h-1V5zm0-2h1v1h-1V3z",
        svgdLocation01: "M253.924,127.592a64,64,0,1,0,64,64A64.073,64.073,0,0,0,253.924,127.592Zm0,96a32,32,0,1,1,32-32A32.037,32.037,0,0,1,253.924,223.592Z",
        svgdLocation02: "M376.906,68.515A173.922,173.922,0,0,0,108.2,286.426L229.107,472.039a29.619,29.619,0,0,0,49.635,0L399.653,286.426A173.921,173.921,0,0,0,376.906,68.515Zm-4.065,200.444L253.925,451.509,135.008,268.959C98.608,213.08,106.415,138.3,153.571,91.142a141.92,141.92,0,0,1,200.708,0C401.435,138.3,409.241,213.08,372.841,268.959Z",
        svgdMoney: "M232,56H24A16,16,0,0,0,8,72V184a16,16,0,0,0,16,16H232a16,16,0,0,0,16-16V72A16,16,0,0,0,232,56ZM75,184,24,140.3V115.7L75,72H181l51,43.7v24.6L181,184Zm93-56a40,40,0,1,1-40-40A40,40,0,0,1,168,128Z",
        svgdUsers: "M12.3,12.22A4.92,4.92,0,0,0,14,8.5a5,5,0,0,0-10,0,4.92,4.92,0,0,0,1.7,3.72A8,8,0,0,0,1,19.5a1,1,0,0,0,2,0,6,6,0,0,1,12,0,1,1,0,0,0,2,0A8,8,0,0,0,12.3,12.22ZM9,11.5a3,3,0,1,1,3-3A3,3,0,0,1,9,11.5Zm9.74.32A5,5,0,0,0,15,3.5a1,1,0,0,0,0,2,3,3,0,0,1,3,3,3,3,0,0,1-1.5,2.59,1,1,0,0,0-.5.84,1,1,0,0,0,.45.86l.39.26.13.07a7,7,0,0,1,4,6.38,1,1,0,0,0,2,0A9,9,0,0,0,18.74,11.82Z",
        svgdCalendar01: "M14 0H2a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2zM1 3.857C1 3.384 1.448 3 2 3h12c.552 0 1 .384 1 .857v10.286c0 .473-.448.857-1 .857H2c-.552 0-1-.384-1-.857V3.857z",
        svgdCalendar02: "M6.5 7a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm-9 3a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm-9 3a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2zm3 0a1 1 0 1 0 0-2 1 1 0 0 0 0 2z",
      };
    },
    methods: {
    getLogoUrl(logo) {
      return this[logo];
    }
  }
  };
  </script>
  
  <style scoped>
  .job-offer {
    width: 97%;
    height: auto;
    min-height: 110px;
    margin-bottom: 16px;
    background-color: whitesmoke;
    display: flex;
    border: 2px;
    font-size: 18px;
    color: black;
    margin-left: 15px;
    border: 2px solid rgba(211, 211, 211, 0.4);
    border-radius: 5px;
    padding-top: 4px;
    padding-bottom: 2px;
    padding-left: 6px;
    padding-right: 15px;
    word-wrap: break-word;
    white-space: pre-wrap;
    overflow-wrap: break-word;
  }

  .job-offer:hover {
    box-shadow: 0 8px 8px rgba(0, 0, 0, 0.2);
  }

  a {
    color: black;
    text-decoration: none;
  }

  .job-img {
    width: 90px;
    height: 90px;
    margin-top: 8px;
    margin-bottom: 8px;
    margin-left: 12px;
    margin-right: 24px;
  }

  .job-details {
    text-align: left;
  }

  .job-title {
    font-size: 22px;
    font-weight: bold;
    margin-right: 20px;
    position: relative;
    top: 12px;
  }

  .skill-list {
    display: inline;
    flex-direction: row;
    position: relative;
    top: 6px;
    left: 2vw;
    word-wrap: break-word;
  }

  .job-skill {
    font-size: 14px;
    font-weight: lighter;
    border: 1px solid black;
    border-radius: 14px;
    padding-top: 2px;
    padding-bottom: 1px;
    padding-left: 4px;
    padding-right: 4px;
    margin-left: 4px;
  }

  .job-specifications {
    display: flex;
    flex-direction: row;
    margin-top: 24px;
    font-size: 15px;
    width: 73vw;
    align-items: center;
  }

  .job-specifications span {
    flex: 1 1 0;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }

  .icon-list {
    text-align: left;
    margin-left: 8px;
    flex-wrap: nowrap;
    padding-top: 4px;
  }

  .icon-extra {
    margin-left: 4px;
    padding-top: 4px;
    padding-bottom: 2px;
    padding-left: 6px;
    padding-right: 6px;
    border: 1px solid black;
    border-radius: 14px;
  }

  @media (max-width: 980px) {
    .job-specifications {
      display: none;
    }
  }
  </style>
