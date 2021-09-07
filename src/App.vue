<template>
  <div id="app">
    <body>

    <ul class="ul1">  
      <h1>{{title}}</h1>
    </ul>

    <ul class="ul2">
      <h2>{{currentDate}}</h2>
    </ul>

      <li v-for="entry in filteredEntries" :key="entry.id"> 
        <ul class="ul3">   
          <h3>{{entry[0]}} Uhr, {{entry[1].replaceAll("/", ".")}}</h3> <br>
          <h4>{{entry[2]}} </h4> <br>
          <h5>{{entry[3]}} </h5>
        </ul></li>

    <ul class="footer">
      <img class="bild1" src="./assets/STZH_SEB_Logo.png" alt="alternativer_text" />
      <img class="bild2" src="./assets/Opportunity.png" alt="alternativer_text" />
      <img class="bild3" src="./assets/SAG_Logo_De.png" alt="alternativer_text" />
    </ul>
    </body>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
        title: "Welcome to Opportunity",
        currentDate : new Date().toISOString().slice(8,10)+"."+new Date().toISOString().slice(5,7)+"."+new Date().toISOString().slice(0,4),
        uhrzeit: "14.00 Uhr",
        gsheet_url: "https://sheets.googleapis.com/v4/spreadsheets/1qLZJwuNv3QmwGhSj1wZZbuXNOkDKN-Ha7fo0Ca_uVVU/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=AIzaSyBesotaNgSaTUIhrSKjEaExdi-ksKInhoE",
        entries: [],
      };
    },
    computed : {
        filteredEntries() {
          return [...this.entries].slice(1); // remove first item of array
        }
    },
    methods: {
      getData() {
        axios.get(this.gsheet_url).then((response) => {
          this.entries = response.data.valueRanges[0].values;
        })
      },
      refreshData() {
        this.getData();
      },
    },
    mounted() {
      this.refreshData();
      setInterval(() => {
        this.refreshData();
      }, 1800000);
    }
}
</script>

<style>

/* css styles go here */
@import url('https://fonts.googleapis.com/css2?family=Inter&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap');

#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

  /* Fonts */

h1 {
  font-family: Inter;
  font-style: bolder;
  font-weight: 900;
  font-size: 62px;
  line-height: 60px;
  color: #323D4A;
}

h2 {
  font-family: Inter;
  font-style: normal;
  font-weight: 500;
  font-size: 50px;
  line-height: 0px;
  color: #9AA7B1;
}

h3 {
  font-family: Inter;
  font-style: normal;
  font-weight: 700;
  font-size: 28px;
  line-height: 20px;
  color: #EB5E00;
  margin: auto;
  padding-left:0px;
  padding-top: 36px;
}
    
h4 {
  font-family: Inter;
  font-style: normal;
  font-weight: 700;
  font-size: 28px;
  line-height: 20px;
  margin: auto;
  padding-left:0px;
  color: rgb(255, 173, 141);
}
    
h5 {
  font-family: Inter;
  font-style: normal;
  font-weight: 500;
  font-size: 28px;
  line-height: 20px;
  margin: auto;
  padding-left:0px;
  color: rgb(255, 173, 141);
}

  /* Divs */

.ul1 {
  width: 764px;
  height: 75px;
  text-align:left;
  margin-left: 20px;
}

.ul2 {
  width: 335px;
  height: 70px;
  text-align:left;
  margin-left: 20px;
}

.ul3 {
  position:relative;
  width: 960px;
  height: 182px;
  margin: auto;
  background: #0F05A0;
  text-align:left;
  margin-top: 35px;
}

  /* Body */

body {
  margin: 0;
  padding: 0;
  width: 1080px;
  height: 1920px;
  background: #E8EFF4;
}

  /* Footer */

.footer {
  position: relative;
  width: 1080px;
  height: 130px;
  left: 0px;
  top: 1790px;
  margin: auto;
  background: #FFFFFF;
  display: flex;
}

  /* Assets */

.bild1 {
  width: 230px;
  height: 44px;
  margin: auto;
}

.bild2 {
  width: 296px;
  height: 55px;
  margin: auto;
}

.bild3 {
  width: 273px;
  height: 52px;
  margin: auto;
}

li {
  list-style-type: none;
}
</style>
