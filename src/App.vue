<template>
  <div>
      <h3>Timer</h3>

    <div>

      <h5>Timer 1</h5>
      <span>{{ formatTime1 }}</span>
      <br>

      <button @click="min1+=1; sec1 =0">+1 m</button>
      <button @click="min1+=5; sec1 =0">+5 m</button>
      <button @click="min1+=10; sec1 =0">+10 m</button>

      <br>
      <button v-on:click="start1" v-if="!timer1On">Start</button>
      <button v-on:click="stop1" v-if="timer1On">Stop</button>
      <button v-on:click="min1 =0; sec1 =0" >Clear</button>
      

    </div>

    <br>


    <div>

      <h5>Timer 2</h5>
      <span>{{ formatTime2 }}</span>
      <br>

      <button @click="min2+=1; sec1 =0">+1 m</button>
      <button @click="min2+=5; sec1 =0">+5 m</button>
      <button @click="min2+=10; sec1 =0">+10 m</button>

      <br>
      <button v-on:click="start2" v-if="!timer2On">Start</button>
      <button v-on:click="stop2" v-if="timer2On">Stop</button>
      <button v-on:click="min2 =0; sec2 =0" >Clear</button>
      

    </div>



    
    <br>
    
  </div>
  
  <hr>

  <!-- <div id="timer">
    <div class="timer">
      <div class="time">
        {{ formatTime }}
      </div>
      <button v-on:click="start" v-if="!timerOn">Start</button>
      <button v-on:click="stop" v-if="timerOn">Stop</button>
    </div>
  </div> -->

  
  
</template>

<script>

export default {

  data(){
    return {

      user: {
        name: 'Nozomu',
        email: '',
        password: ''
      },

      remaining: null,
      fiveMinutes: 60 * 5,

      min: 0,
      sec: 0,
      timerOn: false,
      timerObj: null,

      min1: 0,
      sec1: 0,
      timer1On: false,
      timer1Obj: null,

      min2: 0,
      sec2: 0,
      timer2On: false,
      timer2Obj: null,

      min3: 0,
      sec3: 0,
      timer3On: false,
      timer3Obj: null,
      
    }
  },


  methods:{

    count1: function() {
      if (this.sec1 <= 0 && this.min1 >= 1) {
        this.min1 --;
        this.sec1 = 59;
      } else if(this.sec1 <= 0 && this.min1 <= 0) {
        this.complete1();
      } else {
        this.sec1 --;
      }
    },

    start1: function() {
      let self = this;
      this.timer1Obj = setInterval(function() {self.count1()}, 1000)
      this.timer1On = true
    },

    stop1: function() {
      clearInterval(this.timer1Obj);
      this.timer1On = false
    },

    complete1: function() {
      clearInterval(this.timer1Obj)
    },



    count2: function() {
      if (this.sec2 <= 0 && this.min2 >= 1) {
        this.min2 --;
        this.sec2 = 59;
      } else if(this.sec2 <= 0 && this.min2 <= 0) {
        this.complete1();
      } else {
        this.sec2 --;
      }
    },

    start2: function() {
      let self = this;
      this.timer2Obj = setInterval(function() {self.count2()}, 1000)
      this.timer2On = true
    },

    stop2: function() {
      clearInterval(this.timer2Obj);
      this.timer2On = false
    },

    complete2: function() {
      clearInterval(this.timer2Obj)
    },
  
  },

  computed: {


    formatTime1: function() {
      let timeStrings1 = [
        this.min1.toString(),
        this.sec1.toString()
      ].map(function(str) {
        if (str.length < 2) {
          return "0" + str
        } else {
          return str
        }
      })
      return timeStrings1[0] + ":" + timeStrings1[1]
    },

    formatTime2: function() {
      let timeStrings2 = [
        this.min2.toString(),
        this.sec2.toString()
      ].map(function(str) {
        if (str.length < 2) {
          return "0" + str
        } else {
          return str
        }
      })
      return timeStrings2[0] + ":" + timeStrings2[1]
    },


  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
