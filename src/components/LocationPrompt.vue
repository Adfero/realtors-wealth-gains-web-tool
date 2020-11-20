<template>
  <div class="location-container text-align-center">
    <div class="prompt-container">
      <h2>Where Do You Want To Live?</h2>
      <selectOptions :class="'state-selection'" :options="states" :placeholder='"State"' v-on:input="onChangeState($event)"></selectOptions>
      <selectOptions v-if="selectedState && metroMap[selectedState]" :class="'metro-selection'" :options="metroMap[selectedState]" :placeholder='"Metro Areas"' v-on:input="onChangeMetro($event)"></selectOptions>
      <div class="w-100 mh-2" v-if="selectedState && selectedMetro"><a class="location-next btn-blue btn mt-2" @click="getListings()">Next</a></div>
    </div>
    <div class="illustration realtor">
      <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/realtor-character.svg" />
      <div class="speech-bubble">
        <img class="w-100" src="/wp-content/plugins/realtors-wealth-gains-data-viz/assets/speech-bubble.svg" />
      </div>
    </div>
  </div>
</template>

<script>
import SelectOptions from './SelectOptions'

export default {
  name: 'locationPrompt',
  props: ['data','metroMap','states'],
  data() {
    return {
      selectedState: '',
      selectedMetro: ''
    }
  },
  components: {
    SelectOptions
  },
  methods: {
    getListings(){
      this.$emit('metroSelected', this.selectedMetro)
    },
    getStateFullName(stateAbbr){
      return this.states[stateAbbr]
    },
    onChangeState(event) {
      if(typeof event == "string") {
        this.selectedState = event
      }
    },
    onChangeMetro(event) {
      if(typeof event == "string") {
        this.selectedMetro = event
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../variables.scss';
.location-container {
  min-height: 600px;
  position: relative;
  padding: 0 1rem;
  @media all and (min-width: $screen-sm) {
    min-height: 500px;
  }
  .location-next {
    height: 50px !important;
  }
}

</style>
