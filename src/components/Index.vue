


<template>
<div class="card" >
    
  <header class="card-header" style="background: radial-gradient(circle, rgba(14,8,103,0.5970763305322129) 0%, rgba(186,158,136,1) 35%, rgba(113,136,140,1) 100%);" ><h1 class="title">A tribute to:</h1>
    <p class="card-header-title">
      <b-tag type="is-success" size="is-large">Deleuze</b-tag> <b-tag type="is-success is-light">and</b-tag>
      <b-tag type="is-success" size="is-large">Guattari's</b-tag> 
      -->
            <b-tag type="is-danger" size="is-small">~~~linguistics~~~</b-tag> <b-taglist attached><b-tag type="is-success is-light">by coder</b-tag>---( <b-tag type="is-danger is-light" size="is-large">Emily Burak</b-tag>)---
      <b-tag type="is-success is-light">former philosopher</b-tag></b-taglist>
    </p>
  </header>
    <section>
        <section class="hero is-medium is-bold" style="background: radial-gradient(circle, rgba(14,8,103,0.5970763305322129) 0%, rgba(186,158,136,1) 35%, rgba(113,136,140,1) 100%);">
  <div class="hero-body">
    <div class="container" >
      <h1 class="title">
        Nomadologic Generator
      </h1>
      <h2 class="subtitle">
        A Thousand Plateaus of GPT-2 Text Generation
      </h2>
    </div>
  </div>
</section>
<section style="background: rgb(14,8,103);
background: linear-gradient(90deg, rgba(14,8,103,0.5970763305322129) 0%, rgba(186,158,136,1) 35%, rgba(113,136,140,1) 100%);">
 <b-field position="is-centered">
            <b-input v-model="prefix" placeholder="Speak of nomadology..." type="is-dark" size="is-large">
            </b-input>
            <p class="control">
                <b-button label="Submit" type="is-dark" outlined size="is-large" v-on:click="submitPrefix"/>
            </p>
        </b-field>
         <b-message size="is-medium">
            {{text? text:"and text will appear here"}}
        </b-message>

        <b-loading  :is-full-page="isFullPage" v-model="isLoading" :can-cancel="true">
    <h1 class="title" style="color:#006400; font-size:300%;">Loading...</h1>
        </b-loading>

</section>
      <section class="hero is-small" style="background: radial-gradient(circle, rgba(14,8,103,0.5970763305322129) 0%, rgba(186,158,136,1) 35%, rgba(113,136,140,1) 100%);">
  <div class="hero-body">
    <div class="container">
      <h1 class="title">
        Art credit to <a href="happysleepy.com">Happy Sleepy</a> for the fantastic illustrations
      </h1>
    </div>
  </div>
      </section>

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
    <footer class="footer" style="background: radial-gradient(circle, rgba(14,8,103,0.5970763305322129) 0%, rgba(186,158,136,1) 35%, rgba(113,136,140,1) 100%);">
  <div class="content has-text-centered" >
    <p>
      <strong>Bulma</strong> used for styling, by <a href="https://jgthms.com">Jeremy Thomas</a>. The source code is licensed
      <a href="http://opensource.org/licenses/mit-license.php">MIT</a>. The website content
      is licensed <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/">CC BY NC SA 4.0</a>.
      <strong>Emily Burak</strong> is the <b-tag type="is-success" size="is-small">creator</b-tag> of this page 
      and can be best reached at <a href="https://www.emilytburak.com/">emilytburak.com</a>
    </p>
  </div>
</footer>

    </div>
    
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