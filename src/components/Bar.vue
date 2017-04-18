<template>
  <mu-appbar title="QuranQuiz" class="bar" :zDepth="1">
    <!--<mu-raised-button label="select surah" @click="open" slot="right"/>
    <mu-dialog :open="dialog" title="Select Surah" slot="right" dialogClass="nopad">
      <mu-dropDown-menu :value="this.value" @change="handleChange" autoWidth>
        <mu-menu-item v-for="chapter in chapters" :value="chapter.id" 
        :title="chapter.id + '. ' + chapter.name_simple"/>
        <mu-menu-item value="1" title="1. Al-Fatihah"/>
      </mu-dropDown-menu>
      <span class="divider">-</span>
      <mu-dropDown-menu :value="this.value2" @change="handleChange2" autoWidth>
        <mu-menu-item v-for="chapter in chapters" :value="chapter.id" 
        :title="chapter.id + '. ' + chapter.name_simple"/>
        <mu-menu-item value="1" title="2. Al-Fatihah"/>
      </mu-dropDown-menu>
      <mu-flat-button label="ok" slot="actions" primary @click="close"/>
    </mu-dialog>-->
  </mu-appbar>
</template>

<script>
export default {
  data () {
    return {
      value: '1',
      value2: '1',
      chapters: '',
      dialog: false
    }
  }
}
</script>
