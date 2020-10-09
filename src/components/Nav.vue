<template>
  <div class="container">
      <!-- <div id="localtime">
        <div>Local Date and Time in </div><div className="region">{currentRegion}</div> is <div className="time">{theTime}</div>
      </div> -->  
      <nav>
        <div id="marker"></div>
        <div id="markerbg"></div>
        <ul v-for="location in locations" v-bind:key="location.offset">
          <li>
            <a :id="location.section" @click="activate" :href="location.section" :class="myClass">{{location.label}}</a>
          </li>
        </ul> 
      </nav>
  </div>
</template>

<script>
  export default {
    name: 'Nav',
    data: () => ({
      myClass: false,
      locations: [
        {
          "section": "cupertino",
          "label": "Cupertino",
          "offset": "-7"
        },
        {
          "section": "new-york-city",
          "label": "New York City",
          "offset": "-5"
        },
        {
          "section": "london",
          "label": "London",
          "offset": "0"
        },
        {
          "section": "amsterdam",
          "label": "Amsterdam",
          "offset": "5"
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
          "offset": "10"
        }
      ]
    }),
    methods: {
      indicator: (e) => {
        console.log('indicator called');
        let marker = document.querySelector('#marker');
        //let items = document.querySelectorAll('nav a');

        marker.style.left = e.offsetLeft + "px";
        marker.style.width = e.offsetWidth + "px";

        let navBar = document.querySelector('nav');
        let links = navBar.querySelectorAll('a');

        for (let i = 0; i < links.length; i++) {
          links[i].className = "";
        }
      },
      activate: (e) => {
        e.preventDefault();
        if (e) {
          let navBar = document.querySelector('nav');
          let links = navBar.querySelectorAll('a');

          for (let i = 0; i < links.length; i++) {
            links[i].className = "";
          }
          console.log(e.target.id)
          e.target.className = "active";
        }
      }
    }
  }
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>