<template>
  <div id="app" class="text-center">
    <h1>Word Translator</h1>
    <h5 class="text-muted">Powere By Vue.js</h5>
    <translateForm v-on:formSubmit="translateText"></translateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>

  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
export default {
  name: 'app',
  components: {
    TranslateForm,
    TranslateOutput
  },
  data () {
    return {
      translatedText: ''
    }
  },
  methods: {
    translateText (text, language) {
      const apiURL = 'https://translate.yandex.net/api/v1.5/tr.json/translate'
      const apiKey = 'YOUR-YANDEX-TRANSLATOR-API-KEY-GOES-HERE'
      this.$http.get(apiURL +
        '?key=' + apiKey +
        '&lang=' + language +
        '&text=' + text)
        .then((response) => {
          this.translatedText = response.body.text[0]
        })
    }
  }
}
</script>

<style>
body {
  background:#fefefe
}
</style>
