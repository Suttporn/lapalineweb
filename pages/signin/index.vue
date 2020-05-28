<template></template>

<script>
export default {
  data: () => ({
    CID: '',
    USERID: ''
  }),
  head() {
    return {
      script: [{ src: 'https://static.line-scdn.net/liff/edge/2/sdk.js' }],
      link: [
        {
          rel: 'stylesheet',
          href: 'https://fonts.googleapis.com/css?family=Roboto&display=swap'
        }
      ]
    }
  },

  created() {
    // alert(this.$nuxt.$route.params)
    // this.CID = this.$nuxt.$route.params.CID
    console.log('route', this.$nuxt.$route.params.CID)
  },
  beforeMount() {
    this.CID = this.$nuxt.$route.params.CID
    this.GetProfileLine()
  },
  methods: {
    GetProfileLine() {
      console.log('1654248577-V4x1eMxG', 'ffff')
     var signinn = 'signin ' + this.CID
           
      function initializeLiff(myLiffId) {
        liff
          .init({
            liffId: myLiffId
          })
          .then(() => {
            liff.getProfile().then(p => {
               //alert(p.userId)
              this.USERID = p.userId
            })
            
            liff
              .sendMessages([
                {
                  type: 'text',
                  text: signinn
                }
              ])
              .then(function() {
                liff.closeWindow()
              })
              .catch(function(error) {
                window.alert('Error sending message: ' + error)
              })
          })
      }
      initializeLiff('1654248577-R3KA8WKD')
      
    }
  }
}
</script>

<style>
</style>