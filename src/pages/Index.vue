<template>
  <q-page class="flex flex-center">
    <!-- <img alt="Quasar logo" src="~assets/quasar-logo-full.svg"> -->
    <div class="">
      {{ detail }}
    </div>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',

  data () {
    return {
      // leftDrawerOpen: this.$q.platform.is.desktop
      detail:null,
    }
  },

  methods: {

  },

  mounted() {
    console.log('%c Platform : ', 'color:red',this.$q.platform.is)
    this.detail = this.$q.platform.is
    // var agent = this.header.join(' '),
    //     os = this.matchItem(agent, this.dataos),
    //     browser = this.matchItem(agent, this.databrowser);
    //     console.log('%c This : ', os)

    // return { os: os, browser: browser };
    window.onload = function(){
      document.getElementById('stats').value = getStatsHTML();

      document.getElementById('copyBtn').addEventListener("click", function(){
        select(document.getElementById('stats'));
        copy();
        alert("browser stats copied to clipboard");
      });
    }

    var stats = {
      name: this.$q.platform.name,
      version: this.$q.platform.version,
      layout: this.$q.platform.layout,
      os: this.$q.platform.os,
      product: this.$q.platform.product,
      manufacturer: this.$q.platform.manufacturer,
      description: this.$q.platform.description
    }

    function select(elem){
      elem.focus();
      elem.setSelectionRange(0, elem.value.length);
    }

    function copy(){
      try{
        document.execCommand('copy');
      }
      catch(err){
        console.log("Oops looks like cant use copy to clipboard feature in your device, try to copy the stats manually!");
        console.log(err);
      }
    }

    function getStatsHTML() {

      var statString = "";

      for (var key in stats) {
        if (stats.hasOwnProperty(key)) {
          if (stats[key]) {
            statString += "" + key + " : " + stats[key] + "\n";
            // console.log("" + key + " : " + stats[key]);
          }
        }
      }

      return statString;
    }
  }, // mounted
}
</script>
