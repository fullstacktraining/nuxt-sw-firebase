<template>
  <div class="jumbotron">
    <div class="container">
      <h1 class="display-3">Register</h1>
      <b-form @submit="createUser" @reset="reset">
        <b-form-group
          id="emailInputGroup"
          label="Email address:"
          label-for="emailInput"
        >
          <b-form-input
            id="emailInput"
            type="email"
            v-model="form.email"
            required
            placeholder="Enter email"
          />
        </b-form-group>

        <b-form-group
          id="passwordInputGroup"
          label="Your password:"
          label-for="passwordInput"
        >
          <b-form-input
            id="passwordInput"
            type="password"
            v-model="form.password"
            required
            placeholder="Enter password"
          />
        </b-form-group>

        <b-form-group
          id="password2InputGroup"
          label="Your password again:"
          label-for="password2Input"
        >
          <b-form-input
            id="password2Input"
            type="password"
            v-model="form.password2"
            required
            placeholder="Repeat password"
          />
        </b-form-group>

        <b-button type="submit" variant="success">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      error: '',
      form: {
        email: '',
        password: '',
        password2: ''
      }
    }
  },
  methods: {
    async createUser(evt) {
      evt.preventDefault();
      if (this.form.password !== this.form.password2) {
        this.error = new Error('Passwords do not match');
      } else {
        try {
          await this.$fireAuth.createUserWithEmailAndPassword(
            this.form.email,
            this.form.password
          );
        } catch (error) {
          console.error(error);
        }
      }
    },
    reset(evt) {
      evt.preventDefault();
      this.error = '';
      this.form.email = '';
      this.form.password = '';
      this.form.password2 = '';
    }
  }
}
</script>