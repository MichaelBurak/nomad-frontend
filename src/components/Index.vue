<template>
    <section>
        <section class="hero is-medium is-dark is-bold">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">
        Nomadologic Generator
      </h1>
      <h2 class="subtitle">
        A Thousand Plateaus of GPT-2 Text Generation
      </h2>
    </div>
  </div>
</section>
 <b-field position="is-centered">
            <b-input v-model="prefix" placeholder="Speak of nomadology..." type="is-success" icon="magnify" size="is-large">
            </b-input>
            <p class="control">
                <b-button label="Submit" type="is-dark" outlined size="is-large" v-on:click="submitPrefix"/>
            </p>
        </b-field>
         <b-message size="is-medium">
            {{text}}
        </b-message>

        <b-loading  :is-full-page="isFullPage" v-model="isLoading" :can-cancel="true">
    <h1 class="title" style="color:#006400; font-size:300%;">Loading...</h1>
        </b-loading>

    <b-carousel >
        <b-carousel-item v-for="(carousel, i) in carousels" :key="i" >
            <section :class="`hero is-small is-${carousel.color}`">
                <div class="hero-body centered">
                    <b-image opacity="80%"  :src="carousel.image"/>
                </div>
            </section>
        </b-carousel-item>
    </b-carousel>   
    </section>
</template>


<script>
const axios = require("axios")
export default {
  name: 'Index',
    data(){
        return {
            isLoading: false,
            isFullPage: false,
            prefix: "",
            text:"",
            carousels: [
                { text: 'Slide 1', image:require('../assets/becoming.jpg') },
                { text: 'Slide 2', image:require('../assets/cosmic.jpg') },
                { text: 'Slide 3', image:require('../assets/geology.jpg') },
                { text: 'Slide 4', image:require('../assets/graph.jpg') },
                { text: 'Slide 5', image:require("../assets/subjectobject.png") }
            ]
        }
    },
  methods:{
      submitPrefix:function(){
          var vm = this
          this.isLoading=true
          axios({
    method: 'post',
    url: "https://nomadologic-generator-mj57ujwjhq-uw.a.run.app/",
    data: {
        prefix: this.prefix
    },
    headers: {
        'Content-Type': 'text/plain;charset=utf-8',
    },
}).then(function (response) {
    vm.text = response.data.text
    vm.isLoading=false
}).catch(function (error) {
    console.log(error);
    vm.isLoading=false
});
      },
      
  }
}
</script>