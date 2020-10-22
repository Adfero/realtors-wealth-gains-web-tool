<template>
  <div class="location-container">
    <h2>Where Do You Want To Live?</h2>
    <select name='states' class='dropdown-list states-list' @change="onChangeState($event)">
      <option selected>State</option>
      <option v-for="state in states" :value="state.abbreviation">{{ state.name }}</option>
    </select>
    <select name="avail-metros" class='dropdown-list metro-list' v-if="selectedState" @change="onChangeMetro($event)">
      <option selected>Available Cities</option>
      <option v-for="metro in metroMap[selectedState]" :value="metro.geocode">{{ metro.metroName }}</option>
    </select>
    <a class="location-next button" @click="getListings()">Next</a>
  </div>
</template>

<script>
export default {
  name: 'locationPrompt',
  props: ['data','metroMap','states'],
  data() {
    return {
      selectedState: '',
      selectedMetro: ''
    }
  },
  mounted() {

  },
  methods: {
    getListings() {

    },
    getStateFullName(stateAbbr){
      return this.states[stateAbbr]
    },
    onChangeState(event) {
        this.selectedState = event.target.value
    },
    onChangeMetro(event) {
        this.selectedMetro = event.target.value
        this.$emit('metroSelected', this.selectedMetro)
    }
  }
}
</script>
