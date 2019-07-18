<template>
  <v-layout  justify-space-around row>
    <v-flex xs6 sm3 pt-5>
      <div class="text-xs-center">
        <v-flex pb-3>
          <h3>Correct!</h3>
        </v-flex>
        <v-flex pa-3>
          <h1 class="display-3">し</h1>
        </v-flex>
        <v-flex pa-3>
          <h1 class="display-1">shi</h1>
        </v-flex>
      </div>
    </v-flex>
    <v-flex xs6 sm3 pt-3>
      <v-card min-width="300px">
        <v-card-title class="justify-center" primary-title>
          <div>
            <h1 class="display-4">しゃ</h1>
          </div>
        </v-card-title>
        <v-layout align-center justify-center row fill-height pa-3>
          <v-form row>
            <v-text-field name="answer" label="Answer..." type="text"></v-text-field>
          </v-form>
          <v-btn @click="testChar()" color="orange">Submit</v-btn>
        </v-layout>
      </v-card>
    </v-flex>
    <v-flex xs6 sm3 pt-5>
      <div class="text-xs-center">
        <v-flex pb-3>
          <h3>Progress : </h3>
        </v-flex>
        <v-progress-circular :value="20"></v-progress-circular>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    data: () => ({
      char: [
        ['a', 'あ'],
        ['i', 'い'],
        ['u', 'う'],
        ['e', 'え'],
        ['o', 'お']
      ]
    }),
    props: {
      source: String
    },
    methods:{
      testChar(){
        console.log(this.char)
      }
    }
  }
</script>

