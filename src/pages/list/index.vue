<template>
  <section>
    <div class="test">
      "Vue 微应用列表页"
    </div>
  </section>
</template>

<script>
import fetch from "isomorphic-fetch";

export default {
  name: "List",

  data() {
    return {
      data: [],
      pageInfo: {
        onChange: page => this.fetchVegetable(page, 10)
      },
    }
  },
  
  methods: {
    async fetchVegetable (page, pageSize) {
      const result = await fetch("http://dev-api.jt-gmall.com/mall", {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        // graphql 的查询风格
        body: JSON.stringify({ query: `{ vegetableList (page: ${page}, pageSize: ${pageSize}) { page, pageSize, total, items { _id, name, poster, price } } }` })
      }).then(res => res.json());
      const { vegetableList } = result.data;
      this.data = vegetableList.items;
      this.pageInfo = {
        current: vegetableList.page,
        pageSize: vegetableList.pageSize,
        total: vegetableList.total,
        onChange: page => this.fetchVegetable(page, 10)
      };
    }
  },

  created() {
    this.fetchVegetable(1, 10);
  }
}
</script>
<style lang="scss">
.test {
  color:yellow
}
</style>