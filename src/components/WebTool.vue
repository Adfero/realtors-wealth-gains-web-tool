<template>
  <div class="container m-0">
    <intro v-if="introLoad" @close="goToLocation()"></intro>
    <locationPrompt v-if="location && stateToMetroMap && stateAbbr && sorted" :metroMap="stateToMetroMap" :states="stateAbbr" v-on:metroSelected="updateMetro"></locationPrompt>
    <result v-if="selectedMetro && !location" :data="selectedMetro" @restart="restartToLocation"></result>
    <div class="disclaimer mh-2"><p>The calculations are based on the price of a typical home in the market. The price appreciation depends on a home's condition, and expenditures for a home's upkeep are not factored into these calculations. Home prices have generally increased over time, but home prices can rise or fall dependng national or local economic conditions.</p></div>
  </div>
</template>

<script>
var states =
{
  'AL': 'Alabama',
  'AK': 'Alaska',
  'AZ': 'Arizona',
  'AR': 'Arkansas',
  'CA': 'California',
  'CO': 'Colorado',
  'CT': 'Connecticut',
  'DC': 'District of Columbia',
  'DE': 'Delaware',
  'FL': 'Florida',
  'GA': 'Georgia',
  'HI': 'Hawaii',
  'ID': 'Idaho',
  'IL': 'Illinois',
  'IN': 'Indiana',
  'IA': 'Iowa',
  'KS': 'Kansas',
  'KY': 'Kentucky',
  'LA': 'Louisiana',
  'ME': 'Maine',
  'MD': 'Maryland',
  'MA': 'Massachusetts',
  'MI': 'Michigan',
  'MN': 'Minnesota',
  'MS': 'Mississippi',
  'MO': 'Missouri',
  'MT': 'Montana',
  'NE': 'Nebraska',
  'NV': 'Nevada',
  'NH': 'New Hampshire',
  'NJ': 'New Jersey',
  'NM': 'New Mexico',
  'NY': 'New York',
  'NC': 'North Carolina',
  'ND': 'North Dakota',
  'OH': 'Ohio',
  'OK': 'Oklahoma',
  'OR': 'Oregon',
  'PA': 'Pennsylvania',
  'RI': 'Rhode Island',
  'SC': 'South Carolina',
  'SD': 'South Dakota',
  'TN': 'Tennessee',
  'TX': 'Texas',
  'UT': 'Utah',
  'VT': 'Vermont',
  'VA': 'Virginia',
  'WA': 'Washington',
  'WV': 'West Virginia',
  'WI': 'Wisconsin',
  'WY': 'Wyoming'
};

import Intro from './Intro'
import LocationPrompt from './LocationPrompt'
import Result from './Result'

export default {
  name: 'WebTool',
  data () {
    return {
      isMobile: false,
      introLoad: true,
      prompted: true,
      location: false,
      years: false,
      data: "",
      states: states,
      stateToMetroMap: [],
      stateAbbr: [],
      selectedMetro: '',
      sorted: false
    }
  },
  components: {
    Intro, LocationPrompt, Result
  },
  mounted() {
    // load intro
    var _this = this
    if(this.introLoad){
      this.getData().then(function(returndata){
        return returndata
      });
    }
  },
  methods: {
    goToLocation() {
      this.introLoad = false
      this.location = true
      // when this is called, prep states
    },
    getData() {
      var _this = this
      var $ = jQuery
      return $.getJSON("/wealth-gains-metro-data-json").then(function(data){
        _this.data = data
        if(data !== undefined ) {
          // create new stateToMetroMap array with a state => geocode map
          // see if the current state exists in our returndata; if so, add it to the stateToMetroMap
          var count = Object.keys(data).length
          var i = 0
          // _this.stateAbbr.push({ value: 0, name: "- State -"})
          // _this.stateToMetroMap.push({ value: 0, name: "- Metro -"})
          var bar = new Promise((resolve, reject) => {
            for (var key in data){
              var metroGeocode = key;
              var metroData = data[metroGeocode]
              var metroString = metroData.metro
              var metroStates = metroData.states
              metroStates.forEach(function(metroState,index){
                // verifying validity; excluding US from this
                if(metroState != "US") {
                  if(_this.stateToMetroMap[metroState] === null || !Array.isArray(_this.stateToMetroMap[metroState])) {
                    _this.stateToMetroMap[metroState] = []
                    if(_this.states[metroState] !== undefined){
                      var stateFullName = _this.states[metroState]
                      var stateObj = { value: metroState, name: stateFullName }
                      _this.stateAbbr.push(stateObj)
                    }
                  }
                  var metroObj = { value: metroGeocode, name: metroString }
                  _this.stateToMetroMap[metroState].push(metroObj)
                }
              })
              if (i === count - 1) resolve();
              i++
            }
          })

          bar.then(() => {
            // after done, sort the states by alpha
            _this.stateAbbr = _this.stateAbbr.sort((a, b) => (a.name > b.name) ? 1 : -1)
            _this.sorted = true
            return _this.data
          })
        }
      });
    },
    updateMetro(value){
      this.selectedMetro = this.data[value]
      this.location = false
    },
    restartToLocation() {
      this.introLoad = false
      this.location = true
      this.smoothScrollTo('#app')
    },
    smoothScrollTo(hash){
      var $ = jQuery
      if (hash !== "") {
       $('html, body').animate({
         scrollTop: $(hash).offset().top - 40
       }, 400);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>
