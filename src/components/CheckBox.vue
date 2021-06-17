<template>
  <label>
    <input
      type="checkbox"
      :value="value"
      @change="onChange"
      :checked="checked"
    />
    <span>{{ label }}</span>
  </label>
</template>
<script>
export default {
  name: "CheckBox",
  props: {
    checked: Boolean,
    value: {
      type: String,
      required: false,
      default: () => "",
    },
    label: {
      type: String,
      required: false,
      default: () => "",
    },
  },
  methods: {
    onChange(e) {
      this.$emit("change", e.target.checked);
    },
  },
};
</script>
