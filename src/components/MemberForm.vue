<template>
  <div id="member-form">
    <h1 class="title">{{ heading }}</h1>
    <form @submit.prevent="handleSubmit" class="form">
      <div class="form-wrap">
        <div class="form-group">
          <label>Name</label>
          <input
            ref="first"
            v-model="member.name"
            type="text"
            :class="{ 'has-error': submitting && invalidName }"
            class="form-control"
            @focus="clearStatus"
            @keypress="clearStatus"
          />
        </div>
        <div class="form-group">
          <label for="">Email</label>
          <input
            v-model="member.email"
            type="text"
            :class="{ 'has-error': submitting && invalidEmail }"
            class="form-control"
          />
        </div>
        <div class="form-group">
          <label for="">Phone number</label>
          <input
            v-model="member.phonenumber"
            type="text"
            :class="{ 'has-error': submitting && invalidPhonenumber }"
            class="form-control"
          />
        </div>
        <button class="btn">Add</button>
      </div>
      <div class="validation">
        <small v-if="error && submitting" class="error">
          please fill out all fields ***
        </small>
        <small v-if="success" class="success"> successfully added !!! </small>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'member-form',
  data() {
    return {
      heading: 'Add new member',
      submitting: false, // state check
      error: false,
      success: false,
      member: {
        name: '',
        email: '',
        phonenumber: '',
      },
    }
  },
  methods: {
    handleSubmit() {
      this.submitting = true
      this.clearStatus() // function clearStatus

      if (this.invalidName || this.invalidEmail || this.invalidPhonenumber) {
        this.error = true
        return
      }

      this.$emit('add:member', this.member)
      this.$refs.first.focus()

      this.member = {
        name: '',
        email: '',
        phonenumber: '',
      }

      this.error = false
      this.success = true
      this.submitting = false
    },
    clearStatus() {
      this.success = false
      this.error = false
    },
  },
  computed: {
    invalidName() {
      return this.member.name === ''
    },
    invalidEmail() {
      return this.member.email === ''
    },
    invalidPhonenumber() {
      return this.member.phonenumber === ''
    },
  },
}
</script>

<style lang="scss">
@import '@/assets/styles/components/form.scss';
</style>
