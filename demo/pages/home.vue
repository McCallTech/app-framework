<!-- Initial page of the main view, please see ../app.vue for more information about the application layout -->

<template>
  <f7-page>

    <!-- Navbar -->
    <f7-navbar sliding :title="$root.config.title">
      <f7-nav-right v-if="$root.user"><f7-link icon-material="person" open-popup="#app-framework-login-popup" /></f7-nav-right>
    </f7-navbar>

    <!-- Installation notice -->
    <f7-block inner inset style="text-align: center" v-if="$root.appMode==='mobile'">
      <p><b>For native App feeling, please pin this page to your homescreen and open it from there!</b></p>
    </f7-block>
   <iframe width="100%" height="50%" src="https://www.youtube.com/embed/0L-6ls2Rrgc" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  </f7-page>
</template>

<script>
  module.exports = {
    data: function () {
      return {
        images: {
          flag_en: require('../images/flag-en.png'),
          flag_de: require('../images/flag-de.png'),
          theme_ios: require('../images/theme-ios.png'),
          theme_material: require('../images/theme-material.png'),
          firebase: require('../images/firebase.png')
        }
      }
    },
    methods: {
      updateSmartlist: function (e) {
        setTimeout(function () {
          let text = this.$$(e.target).find('option[value=' + e.target.value + ']').text()
          this.$$(e.target).parent().find('.item-after').html(text)
        }.bind(this), 0)
      }
    }
  }
</script>

<style>
  .f7-icons  {
    width: 29px;
    font-size: 29px;
    height: 29px;
    text-align: center;
    color: gray;
  }
</style>
