<template>
  <div class="container">
      <div id="localtime">
        <div>Local Date and Time in </div>
        <div className="region">{{currentRegion}}</div>
         is 
        <div className="time">{{theTime}}</div>
      </div> 
      <nav>
        <div id="highlite"></div>
        <div id="highlitebg"></div>
        <div v-for="location in locations" :key="location.offset" :data-key="location.offset">
          <a v-text="location.label" @click="activate" :id="location.label" :href="location.section"></a>
        </div>   
      </nav>
  </div>
</template>

<script>
  export default {
    name: 'Nav',
    data: () => ({
      currentRegion: 'Cupertino',
      theTime: '9am',
      offset: '-7', 
      locations: [
        {
          "section": "cupertino",
          "label": "Cupertino",
          "offset": "-7"
        },
        {
          "section": "new-york-city",
          "label": "New York City",
          "offset": "-4"
        },
        {
          "section": "london",
          "label": "London",
          "offset": "1"
        },
        {
          "section": "amsterdam",
          "label": "Amsterdam",
          "offset": "2"
        },
        {
          "section": "tokyo",
          "label": "Tokyo",
          "offset": "9"
        },
        {
          "section": "hong-kong",
          "label": "Hong Kong",
          "offset": "8"
        },
        {
          "section": "sydney",
          "label": "Sydney",
          "offset": "11"
        }
      ]
    }),

    methods: {
      indicator(e) {
        let highlite = document.querySelector('#highlite');
        highlite.style.left = e.srcElement.offsetLeft + "px";
        highlite.style.width = e.srcElement.offsetWidth + "px";

        let navBar = document.querySelector('nav');
        let links = navBar.querySelectorAll('a');

        for (let i = 0; i < links.length; i++) {
          links[i].className = "";
        }
      },

      activate(e) {
        e.preventDefault();
        if (e) {
          let navBar = document.querySelector('nav');
          let links = navBar.querySelectorAll('a');

          for (let i = 0; i < links.length; i++) {
            links[i].className = "";
          }
          
          this.indicator(e);
          this.worstBehavior(e);
          e.target.className = "active";  
        } 
      },

      calculateDateTime() {
        let offset = this.offset;
        // get current local time in milliseconds
        let date = new Date();
        let localTime = date.getTime();
        // get local timezone offset and convert to milliseconds
        let localOffset = date.getTimezoneOffset() * 60000;
        // obtain the UTC time in milliseconds
        let utc = localTime + localOffset;
        let newDateTime = utc + (3600000 * offset);
        let convertedDateTime = new Date(newDateTime);

        return convertedDateTime.toLocaleString();
      },

      worstBehavior(e) { // tribute to Drake for no good reason
        if(e) {
          this.currentRegion = e.target.id;
          this.theTime = '6am';
          this.offset = e.target.parentNode.getAttribute('data-key');
          this.theTime = this.calculateDateTime();
        }
      }
    },
    mounted(){
      document.querySelector('#' + this.locations[0].label).click()
      this.worstBehavior();
    }
  }
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>