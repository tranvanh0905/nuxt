<template>
  <b-container fluid>
    <nuxt-link to="/category/create">
      <b-button variant="success">Add</b-button>
    </nuxt-link>
    <b-table :items="items" :fields="fields">
      <template v-slot:cell(name)="row">
        {{ row.value }}
      </template>
      <template v-slot:cell(actions)="row">
        <b-button variant="danger" @click="onDelete(row)">
          Delete
        </b-button>
      </template>
    </b-table>
  </b-container>
</template>

<script>
export default {
  data() {
    return {
      show     : false,
      urlDelete: [],
      items    : [],
      fields   : [
        {
          key  : 'id',
          label: 'Id',
        },
        {
          key  : 'name',
          label: 'Name',
        },
        {
          key  : 'image',
          label: 'Image',
        },
        {
          key  : 'actions',
          label: 'Actions'
        }
      ],
    }
  },
  methods: {
    async onDelete(data) {
      const id = data.item.id;
      await this.$axios.delete('https://5d2c2c4a8c900700149720a5.mockapi.io/categories/' + id).then((response) => {
        let categories = this.items;
        categories.forEach(function(item, index) {
          if(item.id == id) {
            categories.splice(index, 1)
          }
        })
      })
    },
  },
  async asyncData(content) {
    const {data} = await content.$axios.get('https://5d2c2c4a8c900700149720a5.mockapi.io/categories')
    return {
      items: data,
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand',
  'Source Sans Pro',
  -apple-system,
  BlinkMacSystemFont,
  'Segoe UI',
  Roboto,
  'Helvetica Neue',
  Arial,
  sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
