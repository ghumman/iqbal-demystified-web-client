<template>
  <body class="fixed-nav sticky-footer" id="page-top">

  <nav class="navbar navbar-expand-lg fixed-top" id="mainNav">
      <div class="skew"></div>
      <div class="container">
          <a class="navbar-brand font-weight-bold" href=""><em class="font-weight-bold"> Demystify</em></a>
          <div class="navbar-toggler" data-toggle="collapse" data-target="#navbarsExampleDefault" aria-expanded="false" aria-label="Toggle navigation">
              <i class="text-dark fa fa-ellipsis-h" aria-hidden="true"></i>
          </div>

          <div class="collapse navbar-collapse" id="navbarsExampleDefault">
              <div class="navbar-nav ml-auto my-2 my-lg-0">
                  <a class="nav-item navbar-buttons btn btn-sm my-2 my-sm-0 mr-sm-2" id="add-tutorial"> About </a>
                  <a class="nav-item navbar-buttons btn btn-sm my-2 my-sm-0" href="#login-section"> Signin / Signup </a>
              </div>
          </div>
      </div>
  </nav>

  <div id="vue-app">
      <section id="resource_list" class="mt-5 pt-5 pb-5">
          <div class="container">
              <div class="text-center ml-auto mr-auto col-md-10">
                  <div class="card" id="card">
                      <div class="card-body">
                          <a href=""  class="title-anchor">
                            <h4 v-for="heading in poemDetail.heading">
                              {{heading.text}}
                            </h4>
                          </a>
                          <div v-for="verse in poemDetail.sher" class="card-text pt-3 mb-5" >
                              <p v-for="content in verse.sherContent" v-bind:class="{urdu_text:content.lang=='ur'}" v-html="content"> </p>
                          </div>
                          <div class="social-links">
                              <div class="sharing-links">
                                  <!-- TODO: implement the link sharing -->
                                  <a href="#" class="btn social-twitter"><i class="fa fa-twitter"></i></a>
                                  <a href="#" class="btn social-facebook"><i class="fa fa-facebook"></i></a>
                              </div>
                              <div class="like-this">
                                  <a href="" class="btn like-btn heart_click text-white">{{num_hearts}} <i class="fa fa-heart"></i></a>
                              </div>
                          </div>
                      </div>
                  </div>
              </div>
          </div>
      </section>

      <section id="resource_list" class="pb-5">
          <div class="container">
              <div class="text-center mr-auto ml-auto col-md-10">
                  <div class="card" id="card">

                      <div class="card-body">
                          Comments disabled for now
                      </div>
                  </div>
              </div>
          </div>
      </section>

  </div>

  </body>
</template>

<script>
import StaticContentService from '@/services/StaticContentService'

require('../assets/css/poem_page.css')

export default {
  data () {
    return {
      poemDetail: [],
      num_hearts: 10
    }
  },
  created () {
    this.getPoem(this.$route.query.poemId)
  },
  methods: {
    async getPoem (poemId) {
      const response = await StaticContentService.getPoem(poemId)
      var yamlObject = YAML.parse(response.data)
      this.poemDetail = yamlObject
      console.log(yamlObject)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
