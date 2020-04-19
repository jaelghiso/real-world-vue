<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <input
      id="label"
      :value="value"
      v-on="listeners"
      v-bind="$attrs"
      @input="updateValue"
    />
  </div>
</template>
<script>
import { formFieldMixin } from "../mixins/formFieldMixin";

export default {
  mixins: [formFieldMixin],
  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: this.updateValue,
      };
    },
  },
};
</script>
