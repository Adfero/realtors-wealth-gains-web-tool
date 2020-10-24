<template>
  <div class="location-container text-align-center">
    <div class="prompt-container">
      <h2>Where Do You Want To Live?</h2>
      <select name='states' class='dropdown-list states-list mh-2' @change="onChangeState($event)">
        <option selected>State</option>
        <option v-for="state in states" :value="state.abbreviation">{{ state.name }}</option>
      </select>
      <select name="available-metros" class='dropdown-list metro-list mh-2' v-if="selectedState" @change="onChangeMetro($event)">
        <option selected>Available Cities</option>
        <option v-for="metro in metroMap[selectedState]" :value="metro.geocode">{{ metro.metroName }}</option>
      </select>
      <div class="w-100 mh-2" v-if="selectedState && selectedMetro"><a class="location-next btn-blue btn" @click="getListings()">Next</a></div>
    </div>
    <div class="illustration realtor">
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/js/realtors-wealth-gains/static/assets/realtor-character.svg" />
      <!-- TODO: uncomment this when ready to deploy <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/realtor-character.svg" /> -->
    </div>
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
    getListings(){
      this.$emit('metroSelected', this.selectedMetro)
    },
    getStateFullName(stateAbbr){
      return this.states[stateAbbr]
    },
    onChangeState(event) {
        this.selectedState = event.target.value
    },
    onChangeMetro(event) {
        this.selectedMetro = event.target.value
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../variables.scss';
.location-container {
  min-height: 500px;
  position: relative;
}
.illustration.realtor {
  position: absolute;
  bottom: 0;
  left: 0;
  top: auto;
  right: auto;
}
select.dropdown-list {
  margin: 0 auto;
  display: block;
  border: none;
  border-bottom: 1px solid $color_navy;
  &.states-list {
    font-size: 30px;
  }
  &.metro-list {
    font-size: 22px;
  }
}
</style>
