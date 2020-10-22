<template>
  <div class="container">
    <intro v-if="introLoad" @close="goToLocation()"></intro>
    <locationPrompt v-if="location && stateToMetroMap && stateAbbr" :metroMap="stateToMetroMap" :states="stateAbbr" v-on:metroSelected="updateMetro"></locationPrompt>
    <result v-if="selectedMetro" :data="selectedMetro"></result>
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
      selectedMetro: ''
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
        console.log('so now we hopefully send data to the component',_this.data,_this.stateToMetroMap)
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
      return $.getJSON("http://homeownershipmatters.local/wealth-gains-metro-data-json").then(function(data){
        _this.data = data
        if(data !== undefined ) {
          // create new stateToMetroMap array with a state => geocode map
          // see if the current state exists in our returndata; if so, add it to the stateToMetroMap
          var count = Object.keys(data).length
          var i = 0
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
                    if(_this.states[metroState] !== undefined){
                      _this.stateToMetroMap[metroState] = []
                      var stateFullName = _this.states[metroState]
                      var stateObj = { abbreviation: metroState, name: stateFullName }
                      _this.stateAbbr.push(stateObj)
                    }
                  }
                  var metroObj = { geocode: metroGeocode, metroName: metroString }
                  _this.stateToMetroMap[metroState].push(metroObj)
                }
              })
              if (i === count - 1) resolve();
              i++
            }
          })

          bar.then(() => {
              return _this.data
          })
        }
      });
    },
    updateMetro(value){
      console.log('wooo we got the value',value,this.data[value])
      this.selectedMetro = this.data[value]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
