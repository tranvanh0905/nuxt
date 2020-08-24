<template>
  <div>

    <b-form @submit="onSubmit" v-if="show">
      <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
      },
      show: true
    }
  },
  methods: {
    async onSubmit(e) {
      e.preventDefault()
      await this.$axios.post('https://5d2c2c4a8c900700149720a5.mockapi.io/categories', {
        name : this.form.name,
        image: '',
      }).then((response) => {
        this.$router.push({name: 'category'})
      })
      alert(JSON.stringify(this.form))
    },
  }
}
</script>
