<template>
  <div class="translate container text-center">
    <h2 class="title">Penerjemah</h2>
    <small class="lead">powered by hamba Allah</small>

    <div class="social">
        <span v-for="social in socials" :title="social.title" class="animated zoomOutUp"><a :href=social.link><i :class="social.icon"></i></a></span>
    </div>
    <hr>
    <div class="btn-toolbar">
      <div class="btn-group">
        <a href="#" class="btn btn-default"  v-for='code in codes'  v-on:click="langCode=([code.id,code.name])">{{code.name}}</a>
      </div>
    </div>
    <br>
    <translate-text v-on:submitText="terjemahkanText"></translate-text>
    <translator v-html="textIn"></translator>
  </div>

</template>
<script>

  import TranslateText from './TranslateText'
  import Translator from './Translator'
  export default {
    data() {
      return {
        textIn: '',
        langCode: false,
        socials: [
          {icon: 'fa fa-github', link: 'https://github.com/kunhernowoputra', title: 'Github'},
          {icon: 'fa fa-facebook', link: 'https://www.facebook.com/androiderno', title: 'Facebook'},
          {icon: 'fa fa-twitter', link: 'https://twitter.com/kunhernowoputra', title: 'Twitter'},
          {icon: 'fa fa-soundcloud', link: 'https://soundcloud.com/kun-hernowo-putra', title: 'SoundCloud'},
          {icon: 'fa fa-terminal', link: 'https://kunhernowoputra.github.io/', title: 'Website'},
        ],
        codes: [
          {name: 'Indonesia', id:'id', show:false},
          {name: 'Inggris', id:'en', show:false},
          {name: 'Arab', id:'ar', show:false},
          {name: 'Jerman', id:'da', show:false},
          {name: 'Perancis', id:'fr', show:false},
          {name: 'Belanda', id:'nl', show:false},
          {name: 'Italia', id:'it', show:false},
          {name: 'Korea', id:'ko', show:false},
          {name: 'Russian', id:'ru', show:false}]
      }
    },
    components: {
      'translate-text':TranslateText,
      'translator':Translator
    },
    methods: {
      terjemahkanText(text) {
        let langCode1 = this.langCode[0]
        const api = 'https://translate.yandex.net/api/v1.5/tr.json/translate?lang=id-'+langCode1+'&key=trnsl.1.1.20170510T092840Z.3d5011888b9522c1.1ddc1840c2348dadb09b8461bc6428f132ec1ab9&text='+text
        this.$http.get(api).then(function(response) {
          this.textIn = response.body.text[0]
        })
      }
    }
  }
</script>
<style scoped>

  div.btn-group {
    float: none;
  }
  .available {
    font-size: 100px;
  }
  .social {
    margin-top: 5px;
  }
  .social span a{
    margin-right: 10px;
    margin-left: 10px;
  }
</style>
