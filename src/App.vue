<template>
  <div class="timer">
    <h3>Timer</h3>

    <div class="container">

    

      <div class="timer">

        <strong v-if="!editingNow1">{{title1}}:</strong>
        <button @click="editingNow1 = true" v-if="!editingNow1">Edit name</button>

        <input v-model="title1" v-if="editingNow1">
        <button @click="editingNow1 = false"  v-if="editingNow1">Finish edit</button>

        <br><br>
        <span>{{ formatTime1 }}</span>

        <br><br>

        <button @click="min1+=1; sec1 =0">+1</button>
        <button @click="min1+=5; sec1 =0">5</button>
        <button @click="min1+=10; sec1 =0">10</button>

        <br>
        <button v-on:click="start1" v-if="!timer1On">Start</button>
        <button v-on:click="stop1" v-if="timer1On">Stop</button>
        <button v-on:click="min1 =0; sec1 =0; stop1()" >Clear</button>
        

      </div>
    

      <div class="timer">

        <strong v-if="!editingNow2">{{title2}}:</strong>
        <button @click="editingNow2 = true" v-if="!editingNow2">Edit name</button>

        <input v-model="title2" v-if="editingNow2">
        <button @click="editingNow2 = false"  v-if="editingNow2">Finish edit</button>
        
        <br><br>
        <span>{{ formatTime2 }}</span>
        
        <br><br>

        <button @click="min2+=1; sec1 =0">+1</button>
        <button @click="min2+=5; sec1 =0">5</button>
        <button @click="min2+=10; sec1 =0">10</button>

        <br>
        <button v-on:click="start2" v-if="!timer2On">Start</button>
        <button v-on:click="stop2" v-if="timer2On">Stop</button>
        <button v-on:click="min2 =0; sec2 =0; stop2()" >Clear</button>
        

      </div>

      <div class="timer">

        <strong v-if="!editingNow3">{{title3}}:</strong>
        <button @click="editingNow3 = true" v-if="!editingNow3">Edit name</button>

        <input v-model="title3" v-if="editingNow3">
        <button @click="editingNow3 = false"  v-if="editingNow3">Finish edit</button>
        
        <br><br>
        <span>{{ formatTime3 }}</span>
        
        <br><br>

        <button @click="min3+=1; sec1 =0">+1</button>
        <button @click="min3+=5; sec1 =0">5</button>
        <button @click="min3+=10; sec1 =0">10</button>

        <br>
        <button v-on:click="start3" v-if="!timer3On">Start</button>
        <button v-on:click="stop3" v-if="timer3On">Stop</button>
        <button v-on:click="min3 =0; sec3 =0; stop3()" >Clear</button>
        

      </div>
    </div>

  </div>
  
  <hr>

  <div class="to-do-lis">

    <div class="navbar">
      <ul>
        <li @click="showingPage= 'Abyss'" :class="[showingPage === 'Abyss' ? 'Abyss' : '']"><a >Abyss</a></li>
        <li @click="showingPage= 'Fresh' " :class="[showingPage === 'Fresh' ? 'Fresh' : '']" ><a >Fresh</a></li>
        <li @click="showingPage= 'Hallow'" :class="[showingPage === 'Hallow' ? 'Hallow' : '']"><a >Halloween</a></li>
        <li @click="showingPage= 'Anni'" :class="[showingPage === 'Anni' ? 'Anni' : '']"><a >Annivdersary</a></li>
        <li @click="showingPage= 'Chris'" :class="[showingPage === 'Chris' ? 'Chris' : '']"><a >Christmas</a></li>
        <li style="float:right"><a href="#about">Other</a></li>
      </ul>

    </div>

  </div>

  
  
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

      showingPage: 'Abyss',

      

      remaining: null,
      fiveMinutes: 60 * 5,


      min: 0,
      sec: 0,
      timerOn: false,
      timerObj: null,


      editingNow1: false,
      title1: 'Timer 1',
      min1: 0,
      sec1: 0,
      timer1On: false,
      timer1Obj: null,

      editingNow2: false,
      title2: 'Timer 2',
      min2: 0,
      sec2: 0,
      timer2On: false,
      timer2Obj: null,

      editingNow3: false,
      title3: 'Timer 3',
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
        this.complete2();
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



    count3: function() {
      if (this.sec3 <= 0 && this.min3 >= 1) {
        this.min3 --;
        this.sec3 = 59;
      } else if(this.sec3 <= 0 && this.min3 <= 0) {
        this.complete3();
      } else {
        this.sec3 --;
      }
    },

    start3: function() {
      let self = this;
      this.timer3Obj = setInterval(function() {self.count3()}, 1000)
      this.timer3On = true
    },

    stop3: function() {
      clearInterval(this.timer3Obj);
      this.timer3On = false
    },

    complete3: function() {
      clearInterval(this.timer3Obj)
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

    formatTime3: function() {
      let timeStrings3 = [
        this.min3.toString(),
        this.sec3.toString()
      ].map(function(str) {
        if (str.length < 2) {
          return "0" + str
        } else {
          return str
        }
      })
      return timeStrings3[0] + ":" + timeStrings3[1]
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

.container {
  display: flex;
}
.container > div {
  flex: 1; /*grow*/
}

.container span{
  padding: 0.25em 0.25em;
    /* margin: 5em 5em; */
    font-weight: bold;
    border: solid 3px #000000;
}

.container strong{
  margin-right: 10px;
}

.navbar ul{
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
  font-size: 80%;
}

.navbar li{
  float: left;
  border-right:1px solid #bbb;
  transition: background-color 1s ease;
}

.navbar li:last-child {
  border-right: none;
}

.navbar li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

.navbar li a:hover:not(.active) {
  background-color: #111;
}

.navbar .Abyss {
  background-color: 	dodgerblue;
}

.navbar .Fresh {
  background-color: 	mediumaquamarine;
}

.navbar .Hallow {
  background-color: 	slateblue;
}

.navbar .Anni {
  background-color: 	lightskyblue;
}

.navbar .Chris {
  background-color: 	crimson;
}



</style>
