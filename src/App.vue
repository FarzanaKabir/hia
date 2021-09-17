<template>
  <v-app>
    <Header></Header>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

import Header from "./components/layout/Header";

export default {
  name: 'App',
  components: {
    Header
  },
  data: () => ({
    errorMessages: '',
    name: null,
    formHasErrors: false,
    show: false,
    password: '',
    rules: {
      required: value => !!value || 'Required.',
      min: v => v.length >= 8 || 'Min 8 characters',
      emailMatch: () => (`The email and password you entered don't match`),
    },
  }),

  computed: {
    form() {
      return {
        name: this.name,
        password: this.password

      }
    },
  },

  watch: {
    name() {
      this.errorMessages = ''
    },
  },

  methods: {
    submit() {
      this.formHasErrors = false

      Object.keys(this.form).forEach(f => {
        if (!this.form[f]) this.formHasErrors = true

        this.$refs[f].validate(true)
      })
    },
  },
};
</script>
