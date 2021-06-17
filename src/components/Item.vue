<template>
  <ul v-if="items && items.length">
    <li v-for="item in items" :key="item.id">
      <check-box
        :value="item.id"
        :label="item.title"
        :checked="currentSelected.includes(item.id)"
        @change="(checked) => onCheck(checked, item.id)"
      />
      <item
        v-if="item.items && item.items.length"
        :items="item.items"
        v-model="currentSelected"
      />
    </li>
  </ul>
</template>
<script>
import CheckBox from "./CheckBox.vue";

export default {
  name: "Item",
  components: {
    CheckBox,
  },
  props: {
    items: {
      type: Array,
      required: false,
      default: () => null,
    },
    value: {
      type: Array,
      required: false,
      default: () => [],
    },
  },
  data() {
    return {
      currentSelected: [],
    };
  },
  watch: {
    value(val) {
      this.currentSelected = val;
    },
  },
  methods: {
    onCheck(checked, id) {
      if (checked) {
        this.currentSelected.push(id);
      } else {
        const index = this.currentSelected.findIndex((item) => item === id);
        if (index > -1) {
          this.currentSelected.splice(index, 1);
        }
      }

      this.$emit("input", this.currentSelected);
    },
  },
};
</script>
