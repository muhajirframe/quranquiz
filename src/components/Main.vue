<template>
  <div class="main">
    <Ribbon :title="`Surah ${this.surahName} (${this.surahNumber})`" :subtitle="`Ayat ${this.ayatNumberBegins} - ${this.ayatNumberBegins + 1}`" />
    <Ayat :ayats="ayatContentQuestion[0]" />
    <Ayat :ayats="ayatContentQuestion[1]" />

    <mu-float-button @click="getRandomSurah" icon="replay"
    backgroundColor="#eceff1" class="fab" iconClass="fab-dark-color" />

    <Ribbon title="Ayat Selanjutnya" :subtitle="`Ayat ${this.ayatNumberBegins + 2}`" >
      <mu-raised-button label="Check" @click="isAnswerShown = true" />
    </Ribbon>
    <Ayat v-if="isAnswerShown" :ayats="ayatContentAnswer"/>
  </div>
</template>

<script>
  import Ayat from './Ayat'
  import Ribbon from './Ribbon'
  import axios from 'axios'

  export default {
    name: 'hello',
    data () {
      return {
        isAnswerShown: false,

        ayatNumberBegins: '',
        ayatContentQuestion: '',
        ayatContentAnswer: '',
        surahNumber: '',
        surahName: '',

        minSurah: 1,
        maxSurah: 114
      }
    },
    components: {
      Ayat,
      Ribbon
    },
    methods: {
      getRandom (min, max, fn) {
        const randomNum = Math.floor(Math.random() * (max - min + 1)) + min
        fn(randomNum)
      },
      getRandomSurah () {
        this.answerShown = false

        // Get random surah number
        this.getRandom(this.minSurah, this.maxSurah, randomNumber => {
          this.surahNumber = randomNumber
        })

        // Fetch surah information
        axios.get(`http://staging.quran.com:3000/api/v3/chapters/${this.surahNumber}`)
          .then(response => {
            const maxAyat = response.data.chapter.verses_count
            this.surahName = response.data.chapter.name_simple

            // Set where to begins ayat
            this.getRandom(1, maxAyat - 2, result => {
              this.ayatNumberBegins = result
            })

            // Render the ayats
            this.printAyat()
          })
      },
      printAyat () {
        axios.get(`http://staging.quran.com:3000/api/v3/chapters/${this.surahNumber}/verses`, {
          params: {
            offset: this.ayatNumberBegins - 1,
            limit: 3,
            text_type: 'image'
          }
        })
          .then(response => {
            const verses = response.data.verses
            console.log(response)
            this.ayatContentQuestion = verses.slice(0, 2).map(item => item.text_madani)
            this.ayatContentAnswer = verses[2].text_madani
          })
      }
    },
    created () {
      this.getRandomSurah()
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .main {
    padding-top: 7rem;
    padding-bottom: 10rem;
  }
  
  .question {
    /*background-color: #2196f3;*/
    min-height: 30rem;
    font-size: 2rem;
  }
  
  .fab {
    background-color: #fff;
    position: fixed;
    z-index: 100;
    right: 3rem;
    bottom: 5rem;
  }
</style>

<style>
  .fab-dark-color {
    color: #555;
  }
</style>
