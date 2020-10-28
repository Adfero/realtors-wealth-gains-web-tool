<template>
  <div class="custom-select mh-2" :tabindex="tabindex" @blur="open = false">
    <div class="selected" :class="{ open: open }" @click="open = !open" :data-select-val="selected.value">
      {{ selected.name }}
    </div>
    <div class="items" :class="{ selectHide: !open }">
      <div
        v-for="(option, i) of options"
        :key="i"
        :data-option-value="option.value"
        @click="
          selected = option;
          open = false;
          $emit('input', option.value);
        "
      >
        {{ option.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'selectOptions',
  props: {
    options: {
      type: Array,
      required: true,
    },
    default: {
      type: String,
      required: false,
      default: { name: 'State', value:0 },
    },
    tabindex: {
      type: Number,
      required: false,
      default: 0,
    },
    placeholder: ''
  },
  data() {
    return {
      selected: this.default
        ? this.default
        : this.options.length > 0
        ? 0
        : null,
      open: false,
    };
  },
  mounted() {
    this.default.name = this.placeholder
    this.$emit("input", this.selected)
  },
};
</script>

<style lang="scss" scoped>
@import '../variables.scss';
.custom-select {
  position: relative;
  max-width: 400px;
  text-align: left;
  outline: none;
  // height: 47px;
  line-height: 4rem;
  margin: 0 auto;
  font-size: 3rem;
  text-align: center;
  font-family: $font_brandon;
  &.metro-selection {
    font-size: 2.5rem;
  }
}

.custom-select .selected {
  background-color: $color_white;
  border-radius: 0;
  border: none;
  border-bottom: 1px solid $color_navy;
  color: $color_navy;
  // padding-left: 1em;
  cursor: pointer;
  user-select: none;
  padding: 0 15px;
}

.custom-select .selected.open {
  border: 1px solid #ad8225;
  border-radius: 6px 6px 0px 0px;
}

.custom-select .selected:after {
  content: '\25BE';
  position: absolute;
  right: 0;
  width: 20px;
  bottom: 27px;
  height: 20px;
  font-size: 20px;
  border: 5px solid transparent;
  border-color: #fff transparent transparent transparent;
}

.custom-select .items {
  color: $color_white;
  text-align: left;
  border-radius: 0px 0px 6px 6px;
  overflow: hidden;
  border-right: 1px solid $color_white;
  border-left: 1px solid $color_white;
  border-bottom: 1px solid $color_white;
  position: absolute;
  background-color: $color_navy;
  left: 0;
  right: 0;
  z-index: 1;
  font-size: 2.5rem;
  max-height: 350px;
  overflow-y: scroll;
}

.custom-select .items div {
  color: $color_white;
  background-color: $color_navy;
  // padding-left: 1em;
  cursor: pointer;
  user-select: none;
  padding: 5px 15px;
}

.custom-select .items div:hover {
  background-color: $color_green;
}

.selectHide {
  display: none;
}
</style>
