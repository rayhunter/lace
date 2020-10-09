<template>
  <div class="container">
      <!-- <div id="localtime">
        <div>Local Date and Time in </div><div className="region">{currentRegion}</div> is <div className="time">{theTime}</div>
      </div> -->  
      <nav>
        <div id="marker"></div>
        <div id="markerbg"></div>
        <ul v-for="location in locations" v-bind:key="location.offset">
          <li><a href="#">{{location.label}}</a></li>
        </ul>
      </nav>
  </div>
</template>

<script>
  export default {
    name: 'Nav',
    data: () => ({
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
    })
  }
</script>

<style>
  h3 {
    margin-bottom: 5%;
  }
</style>