<template>
  <v-app>

    <v-content>
      <HelloWorld></HelloWorld>
      <v-layout row wrap>
        <v-flex xs12 sm6 md4>
          <v-text-field
            hint="City,Country Code"
            label="Please enter your city here"
            single-line
            outline
            v-model="cityRequest"
          ></v-text-field>
        </v-flex>
        <v-flex xs12 sm6 md4>
          <v-btn @click="requestCity">Request Weather Data</v-btn>
        </v-flex>
        <v-flex xs12 sm6 md4>
          <v-text-field
            v-model="outputData"
            auto-grow
            textarea
          ></v-text-field>
        </v-flex>
</v-layout>
    </v-content>

    <v-footer :fixed="fixed" app>
      <span>&copy; 2018</span>
    </v-footer>
  </v-app>
</template>

<style>
  textarea {
    width: 100%;
  }
  span {
    padding-left: 10px;
  }
</style>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld,

  },
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'bubble_chart',
        title: 'Inspire'
      }],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
      first: 'John',
      last: 'Doe',
      cityRequest: '',
      outputData: '',

    }
  },
  methods: {
    requestCity(){
      let inputString = 'http://api.openweathermap.org/data/2.5/weather?q=' + this.cityRequest +'&appid=ab45b5b8de7f40499e679726a1e39407'
      let request = this.$axios.get(inputString).then((response) => {
        this.outputData = JSON.stringify(response);
        return response;
      });
      return request;
    }
  },
}
</script>
