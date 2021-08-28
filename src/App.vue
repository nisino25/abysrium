<template>
  <div>
    <div class="timer">
    <h3>Timer</h3>

    <div class="container">

    

      <div class="timer">

        <strong v-if="!editingNow1">{{title1}}:</strong>
        <button @click="editingNow1 = true" v-if="!editingNow1">Edit name</button>

        <input v-model="title1" v-if="editingNow1">
        <button @click="editingNow1 = false"  v-if="editingNow1">Finish edit</button>

        <br><br>
        <span :style="{border: borderColor1}">{{ formatTime1 }}</span>

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
        <span :style="{border: borderColor2}">{{ formatTime2 }}</span>
        
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
        <span :style="{border: borderColor3}">{{ formatTime3 }}</span>
        
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

  <div>

    <div class="navbar">
      <ul>
        <li @click="showingPage= 'Abyss'" :class="[showingPage === 'Abyss' ? 'Abyss' : '']" ><a >Abyss</a></li>
        <li @click="showingPage= 'Fresh' " :class="[showingPage === 'Fresh' ? 'Fresh' : '']" ><a >Fresh</a></li>
        <li @click="showingPage= 'Hallow'" :class="[showingPage === 'Hallow' ? 'Hallow' : '']"><a >Halloween</a></li>
        <li @click="showingPage= 'Anni'" :class="[showingPage === 'Anni' ? 'Anni' : '']"><a >Annivdersary</a></li>
        <li @click="showingPage= 'Chris'" :class="[showingPage === 'Chris' ? 'Chris' : '']"><a >Christmas</a></li>
        <li @click="showingPage= 'pubg'" :class="[showingPage === 'pubg' ? 'pubg' : '']"><a >Pubg</a></li>
        <li style="float:right"><a href="#about">Other</a></li>
      </ul>

    </div>

    <div class="to-do-list" >
      <h4>To-do-list</h4>
      <!-- <button @click="openingModal = true">Add task</button> -->

      <div id="myDIV" class="header " :style="bgc">
        <h2 style="margin:5px">My To Do List</h2>
        <input type="text" id="myInput" placeholder="Reminde Title.." v-model="inputText">
        <span @click="AddTask(showingPage)" class="addBtn">Add</span>
        <input type="number" id="myInput" placeholder="Times..." v-model="inputNum">
        <span  class="addBtn">Times</span>
        <!-- <span  class="addBtn" @click="test('Abyss')">Times</span> -->
        
      </div>

      <ul id="myUL" v-for="(task, i) in TaskList.[showingPage]" :key="i">

        <div v-if="task.showing">
          <li @click="task.currentNum++" v-if="task.currentNum < task.goalNum">{{task.title}}: {{task.currentNum}}/{{task.goalNum}}</li>
          <li @click="deleteTask(showingPage, i)" v-else style="background: #888">{{task.title}}: {{task.currentNum}}/{{task.goalNum}}</li>
        </div>
        
        
      </ul>



      <div class="abyss">

        
      </div>


    </div>

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
      
      inputNum:1,
      inputText: '',

      bgc: 'background-color: 	dodgerblue;',

      TaskList:{Abyss:[], Fresh:[], Hallow:[], Anni:[], Chris:[], pubg:[]},
      

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
      borderColor1: 'solid 3px black',

      editingNow2: false,
      title2: 'Timer 2',
      min2: 0,
      sec2: 0,
      timer2On: false,
      timer2Obj: null,
      borderColor2: 'solid 3px black',

      editingNow3: false,
      title3: 'Timer 3',
      min3: 0,
      sec3: 0,
      timer3On: false,
      timer3Obj: null,
      borderColor3: 'solid 3px black',
      
    }
  },


  methods:{

    AddTask(name){
      if(this.inputNum == 0 || this.inputText == ''){
        return
      }
      // this.results.push({time: Date.now(),outcome: Number(this.currentTime) });
      this.TaskList.[name].push({goalNum: this.inputNum, currentNum: 0, title: this.inputText,finishd: false,showing: true});
      console.log(this.TaskList.[name])

      this.inputNum = 1;
      this.inputText = '';
    },

    deleteTask(name,i){
      let r= confirm(`Deleting [${this.TaskList.[name].[i].title}]...`);
      if(r){
        this.TaskList.[name].[i].showing = false;
        return;
      }
    },



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
      this.borderColor1 = 'solid 3px black';
    },
    complete1: function() {
      this.borderColor1 = 'solid 3px red';
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
      this.borderColor2 = 'solid 3px black';
    },
    complete2: function() {
      this.borderColor2 = 'solid 3px red';
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
      this.borderColor3 = 'solid 3px black';
    },
    complete3: function() {
      this.borderColor1 = 'solid 3px red';
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
          // this.borderColor1 = 'solid 3px orange';
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
          // this.borderColor2 = 'solid 3px orange';
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
          // this.borderColor3 = 'solid 3px orange';
          return "0" + str
        } else {
          return str
        }
      })
      return timeStrings3[0] + ":" + timeStrings3[1]
    },


  },

  watch:{

    showingPage: function(){
      switch (this.showingPage) {

        case 'Abyss':
          this.bgc = 'background-color: 	dodgerblue';
          break;

        case 'Fresh':
          this.bgc = 'background-color: mediumaquamarine';
          break;

        case 'Hallow':
          this.bgc = 'background-color: 	slateblue'
          break;

        case 'Anni':
          this.bgc = 'background-color: 	lightskyblue';
          break;

        case 'Chris':
          this.bgc = 'background-color: 	crimson';
          break;

        case 'pubg':
          this.bgc = 'background-color: 	coral';
          break;
        

        

        case 'Papayas':
          console.log('Mangoes and papayas are $2.79 a pound.');
          // expected output: "Mangoes and papayas are $2.79 a pound."
          break;

        default:
          alert('wff is the input')
      }

    },

    TaskList: {
      deep:true,
      handler() {
        localStorage.TaskList = JSON.stringify(this.TaskList); 
        console.log('touched lsit')
      },
    }

  },

  mounted() {
    if (localStorage.TaskList) {
      this.TaskList = JSON.parse(localStorage.TaskList);
      console.log('getting data')
    }else{
      console.log('nothugn here')
    }
  },
      
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 15px;
  touch-action: manipulation;

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

.yellow-border{
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
  font-size: 50%;
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

/* .navbar li a:hover:not(.active) {
  background-color: #111;
} */

.navbar .Abyss, .Abyss {
  background-color: 	dodgerblue;
}

.navbar .Fresh, .Fresh {
  background-color: 	mediumaquamarine;
}

.navbar .Hallow, .Hallow {
  background-color: 	slateblue;
}

.navbar .Anni, .Anni {
  background-color: 	lightskyblue;
}

.navbar .Chris, .Chris{
  background-color: 	crimson;
}

.navbar .pubg, .pubg {
  background-color: 	coral;
}


/* ---------- */

body {
  margin: 0;
  min-width: 250px;
}

/* Include the padding and border in an element's total width and height */
* {
  box-sizing: border-box;
}

/* Remove margins and padding from the list */
.to-do-list ul {
  margin: 0;
  padding: 0;
}

/* Style the list items */
.to-do-list ul li {
  cursor: pointer;
  position: relative;
  padding: 12px 8px 12px 40px;
  list-style-type: none;
  background: #eee;
  font-size: 18px;
  transition: 0.2s;
  
  /* make the list items unselectable */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Set all odd list items to a different color (zebra-stripes) */
.to-do-list ul li:nth-child(odd) {
  background: #f9f9f9;
}

/* Darker background-color on hover */
.to-do-list ul li:hover {
  background: #ddd;
}

/* When clicked on, add a background color and strike out text */
.to-do-list ul li.checked {
  background: #888;
  color: #fff;
  text-decoration: line-through;
}

/* Add a "checked" mark when clicked on */
.to-do-list ul li.checked::before {
  content: '';
  position: absolute;
  border-color: #fff;
  border-style: solid;
  border-width: 0 2px 2px 0;
  top: 10px;
  left: 16px;
  transform: rotate(45deg);
  height: 15px;
  width: 7px;
}

/* Style the close button */
.close {
  position: absolute;
  right: 0;
  top: 0;
  padding: 12px 16px 12px 16px;
}

.close:hover {
  background-color: #f44336;
  color: white;
}

/* Style the header */
.header {
  background-color: ;
  padding: 30px 40px;
  color: white;
  text-align: center;
}

/* Clear floats after the header */
.header:after {
  content: "";
  display: table;
  clear: both;
}

/* Style the input */
.to-do-list input {
  margin: 0;
  border: none;
  border-radius: 0;
  width: 75%;
  padding: 10px;
  float: left;
  font-size: 16px;
}

/* Style the "Add" button */
.addBtn {
  padding: 10px;
  width: 25%;
  background: #d9d9d9;
  color: #555;
  float: left;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
  border-radius: 0;
}

.addBtn:hover {
  background-color: #bbb;
}







</style>
