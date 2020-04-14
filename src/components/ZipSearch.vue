<template>
  <ion-grid>
    <form @submit="onSubmit">
      <ion-col>
        <ion-item>
          <ion-label>ZipCode:</ion-label>
          <ion-input
            :value="zip"
            @input="zip= $event.target.value"
            placeholder="Enter US ZipCode" />
        </ion-item>
      </ion-col>
      <ion-col>
        <ion-button type="submit" color="primary" expand="block">
          Find
        </ion-button>
      </ion-col>
    </form>
  </ion-grid>
</template>

<script>
export default {
  name: 'zipSearch',
  data() {
    return {
      zip: ''
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()
      const reg = /(^\d{5}$)|(^\d{5}-\d{4}$)/
      const isValid = reg.test(this.zip)
      if (!isValid) {
        this.showAlert()
        return
      }
      this.$emit('get-zip', this.zip)
      this.zip = ''
    },
    showAlert() {
      return this.$ionic.alertController.create({
        header: 'Enter zipcode',
        message: 'Please enter a valid US zipcode',
        buttons: ['ok']
      }).then(a => a.present())
    }
  }
}
</script>
