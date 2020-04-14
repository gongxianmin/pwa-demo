<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>
          ZipInfo
        </ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch @get-zip="getZipInfo"></ZipSearch>
      <ZipInfo :info="info"></ZipInfo>
      <ClearInfo :info="info" @clear-info="clearInfo"></ClearInfo>
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from '@/components/ZipSearch'
import ZipInfo from '@/components/ZipInfo'
import ClearInfo from '@/components/ClearInfo'
export default {
  name: 'home',
  data() {
    return {
      info: null
    }
  },
  components: {
    ZipSearch,
    ZipInfo,
    ClearInfo
  },
  methods: {
    async getZipInfo(zip) {
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`)
      if (res.status === 404) {
        this.showAlert()
      }
      this.info = await res.json()
    },
    showAlert() {
      return this.$ionic.alertController.create({
        header: 'Enter zipcode',
        message: 'Please enter a valid US zipcode',
        buttons: ['ok']
      }).then(a => a.present())
    },
    clearInfo() {
      this.info = null
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
