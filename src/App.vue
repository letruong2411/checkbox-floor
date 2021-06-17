<template>
  <div>
    <div class="count">Count: {{ count }}</div>
    <div class="block" v-for="item in data" :key="item.id">
      <h2>{{ item.title }}</h2>
      <block-item
        :item="child"
        v-for="child in item.items"
        :key="child.id"
        @change="onChange"
      />
    </div>
  </div>
</template>

<script>
import BlockItem from "./components/BlockItem.vue";

export default {
  name: "App",
  components: {
    BlockItem,
  },
  data() {
    return {
      selected: {},
      data: [
        {
          id: "1",
          title: "Heading 1",
          items: [
            {
              id: "1-1",
              heading: "Heading 1-1",
              title: "All 1-1",
              items: [
                {
                  id: "1-1-1",
                  title: "Item 1-1-1",
                },
                {
                  id: "1-1-2",
                  title: "Item 1-1-2",
                },
                {
                  id: "1-1-3",
                  title: "Item 1-1-3",
                },
              ],
            },
            {
              id: "1-2",
              heading: "Heading 1-2",
              title: "All 1-2",
              items: [
                {
                  id: "1-2-1",
                  title: "Item 1-2-1",
                },
                {
                  id: "1-2-2",
                  title: "Item 1-2-2",
                },
                {
                  id: "1-2-3",
                  title: "Item 1-2-3",
                },
              ],
            },
          ],
        },
        {
          id: "2",
          title: "Heading 2",
          items: [
            {
              id: "2-1",
              title: "Item 2-1",
              items: [
                {
                  id: "2-1-1",
                  title: "Item 2-1-1",
                },
              ],
            },
            {
              id: "2-2",
              title: "Item 2-2",
            },
            {
              id: "2-3",
              title: "Item 2-3",
            },
            {
              id: "2-4",
              title: "Item 2-4",
            },
            {
              id: "2-5",
              title: "Item 2-5",
            },
          ],
        },
      ],
    };
  },
  computed: {
    count() {
      let count = 0;
      const values = Object.values(this.selected);

      values?.forEach((item) => {
        count += item.length;
      });
      return count;
    },
  },
  methods: {
    onChange({ id, selected }) {
      this.selected = {
        ...this.selected,
        [id]: selected,
      };
    },
  },
};
</script>
<style>
.h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 8px 0;
}

.block {
  background: plum;
  padding: 8px;
}

.block__item {
  background: yellow;
  padding: 8px;
}

.block__item + .block__item {
  margin-top: 8px;
}

ul {
  list-style: none;
  padding: 0;
}

ul > li > ul {
  margin-left: 24px;
}

ul > li,
li + li {
  margin-top: 8px;
}
.count {
  position: sticky;
  top: 0;
  z-index: 1;
  padding: 16px;
  background: white;
}
</style>
