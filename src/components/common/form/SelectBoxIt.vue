<template>
  <select>
    <option v-for="option in options"
            :value="option.id"
            :key="option.id">
      {{ option.name }}
    </option>
  </select>
</template>

<script>
import Vue from 'vue';

export default {
  name: 'SelectBoxIt',
  props: ['options', 'value'],

  mounted() {
    const vm = this;
    $(this.$el)
      .selectBoxIt()
      .val(this.value)
      .trigger('change')
      .on('change', function emitEventOnChange() {
        vm.$emit('input', this.value);
      });
  },
  watch: {
    value(value) {
      // update value
      $(this.$el).val(value).trigger('change');
    },

    options() {
      Vue.nextTick(() => $(this.$el).data('selectBox-selectBoxIt').refresh());
    },
  },
};
</script>

<style>
.selectboxit-container {
  display: block;
}
</style>
