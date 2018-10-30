<template>
  <v-layout
    column
    justify-center
    align-center>
    <v-flex
      xs12
      sm8
      md6>
      <div class="text-xs-center">
      </div>
      <v-card>
        <v-card-title class="headline">Welcome to the Vuetify + Nuxt.js template</v-card-title>
        <v-card-text>
          <div>
          <p>ランダムな数字だよ（FlaskのAPIから非同期で取得してるよ）: {{ randomNumber }}</p>
          <v-btn
            :loading="loading"
            :disabled="loading"
            color="secondary"
            @click.native="loader='loading'"
            @click="getRandom"
          >
          ランダムナンバー取得
          </v-btn></div>
            <form><v-textarea
            outline
            name="input-7-4"
            label="テキストエリア"
            v-model="message"
            ></v-textarea>
          <v-btn type="submit" @click.stop.prevent="submit()">submit</v-btn>
          <v-btn @click="clear">clear</v-btn></form>
        </v-card-text>
        <v-card-actions>
          <v-spacer/>
            <v-btn
              color="primary"
              flat
              nuxt
              to="/inspire">Continue</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'

export default {
  components: {
  },
  data() {
    return{
      randomNumber: 0,
      message: ''
    }
  },
  methods: {
    async getRandom(){
      const res = await this.$axios.get('http://localhost:5000/api/random');
      this.randomNumber=res.data.randomNumber
    },
    clear(){
      this.message = '';
    },
    submit(){
      this.$router.push("search?" + this.message); 
    }
  },
}
</script>
