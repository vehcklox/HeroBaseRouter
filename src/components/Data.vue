<template>
  <div class="col-md-12">
    <Item
      v-for="(item, index) in items"
      :key="index"
      :passed-item="item"
      :type="type"
    />
  </div>
</template>

<script>
  import Item from './Item';

  export default {
    data() {
      return {
        type: this.$route.params.type,
        items: [],
      }
    },
    methods: {
      fetchItems() {
        this.items = [];
        this.type = this.$route.params.type;
        let initial_ids = [1, 4, 7];
        for (let i in initial_ids) {
          let id = initial_ids[i];
          fetch(
            `https://lotrapi.co/api/v1/${this.type}/${id}`, {
              method: 'GET'
            })
            .then(response => response.json())
            .then(json => this.items.push(json))
        }
      }
    },
    created() {
      this.fetchItems()
    },
    components: {
      Item
    },
    watch: {
      '$route': 'fetchItems'
    }
  }
</script>
