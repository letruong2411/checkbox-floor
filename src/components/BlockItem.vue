<template>
  <ul class="block__item">
    <h4 v-if="item.heading">{{ item.heading }}</h4>
    <li>
      <check-box
        :value="item.id"
        :label="item.title"
        :checked="isChecked"
        @change="onCheck"
      />
      <item
        v-if="item.items && item.items.length"
        :items="item.items"
        v-model="selected"
      />
    </li>
  </ul>
</template>
<script>
import Item from "@/components/Item";
import CheckBox from "./CheckBox";

export default {
  name: "BlockItem",
  props: {
    item: {
      type: Object,
      required: false,
      default: () => null,
    },
    value: {
      type: Array,
      required: false,
      default: () => [],
    },
  },
  components: {
    Item,
    CheckBox,
  },
  data() {
    return {
      isSelected: false,
      selected: [],
    };
  },
  computed: {
    hasChild() {
      return !!this.item.items?.length;
    },
    isChecked() {
      return this.hasChild
        ? this.item.items.length === this.selected.length
        : this.isSelected;
    },
  },
  watch: {
    selected(val) {
      this.$emit("input", val);
      this.$emit("change", {
        id: this.item.id,
        selected: val,
      });
    },
  },
  methods: {
    onCheck(checked) {
      this.isSelected = checked;

      if (checked) {
        this.selected = this.hasChild
          ? this.item.items.map((item) => item.id)
          : [this.item.id];
      } else {
        this.selected = [];
      }
    },
  },
};
</script>
