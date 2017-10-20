<template>
  <div id="app">

    <h1>Vuemon</h1>

    <div id="simon">

      <div id="status">
        
    </div>
      <div id="youlose">
        <h2>{{ loser }}</h2>
      </div>
      <div class="row">
        <div id="green" class="light col" v-bind:class="{ 'active': activeGreen }" v-on:click="captureTap('green')"></div>
        <div id="red" class="light col" v-bind:class="{ 'active': activeRed }" v-on:click="captureTap('red')"></div>
      </div>

      <div class="row">
        <div id="yellow" class="light col" v-bind:class="{ 'active': activeYellow }" v-on:click="captureTap('yellow')"></div>
        <div id="blue" class="light col" v-bind:class="{ 'active': activeBlue }" v-on:click="captureTap('blue')"></div>
      </div>

    </div>

    <div id="controls" class="row">
      <div class="col"><button class="start" v-on:click="start">Start</button></div>
    </div>

    <div id="history">
      <p><strong>Current Sequence:</strong> {{ current }}</p>
      <p><strong>Longest Sequence:</strong> {{ longest }}</p>
    </div>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      longest: 0,
      sequence: ['red', 'green', 'yellow', 'blue'],
      taps: [],
      lights: [ 'red', 'green', 'yellow', 'blue' ],
      activeGreen: false,
      activeBlue: false,
      activeYellow: false,
      activeRed: false,
      litcounter:0,
      countTaps:0,
      loser: ""
      
    }
    
  },
  computed: {
    current: function() {
      return this.sequence.length;
    }
  },
  mounted() {

  },
  methods: {

    // isActive: function(litUp) {
    //   return this.activeItem === litUp;

    // },

    setToFalse : function() {
      setTimeout(function() {
        this.activeYellow=false;
        this.activeRed=false;
        this.activeBlue=false;
        this.activeGreen=false;
      }.bind(this), arguments[0]);

    },

    captureTap: function() {
      this.setToFalse(250);
      switch(arguments[0]) {
        case "red":
          this.activeRed = true;
        break;
        case "green":
          this.activeGreen=true;
        break;
        case "blue":
          this.activeBlue=true;
        break;
        case "yellow":
          this.activeYellow=true;
        break;
        };
      this.taps.push(arguments[0]);

      // logic for processing game 

      //console.log(this.taps[0]);  
      //console.log(this.sequence);
      this.compareUserInput();
      
    },

    compareUserInput : function() {
      
      //co (nsole.log(this.sequence[1]);
      //for (var i = 0; i < this.sequence.length; i++) {
        if (this.taps[this.countTaps] == this.sequence[this.countTaps]) {
          (this.countTaps++);
          console.log("taps=Sequence");
        }
        if (this.countTaps == this.sequence.length) {
          console.log("Winner");
        }
        else {
          this.loser="Absolutely pathetic!! You are not worthy of the VUEmon!";

        }
        //console.log(this.countTaps);
      //}
    },

    start: function() {
      //this.sequence = [];
      this.addToSequence();
      this.playSequence();
      //console.log(this.sequence[this.litcounter]);
      //this.sequence;
      this.litcounter=0;
      // this.startTime();
      this.taps=[];
      this.loser="";
    },

    chooseRandomLight: function() {
      var index = Math.floor(Math.random() * 4);
      //console.log(this.lights[index]);
      return this.lights[index];
      //console.log(this.lights[index]);
    },

    addToSequence: function() {
      this.sequence.push(this.chooseRandomLight());
            console.log(this.sequence); 

    },

    playSequence: function() {
      setTimeout(function () {
        this.activeYellow=false;
        this.activeRed=false;
        this.activeBlue=false;
        this.activeGreen=false;
        switch(this.sequence[this.litcounter]) {
          case "red":
            this.activeRed = true;
            break;
          case "green":
            this.activeGreen=true;
            break;
          case "blue":
            this.activeBlue=true;
            break;
          case "yellow":
            this.activeYellow=true;
              break;
          };
        this.litcounter++;
        if (this.litcounter < this.sequence.length) {                  
          this.playSequence();           
        }
        else {
          this.setToFalse(100);
          console.log("done");
        }
      }.bind(this), 100);
    }  
  }
}
  



</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

#simon {
  padding: 20px;
}

#controls {
  padding-bottom: 20px;
}

#status {
  padding-bottom: 20px;
}

.row {

}

.col {
  display: inline-block;
}

.start {
  padding: 10px;
  font-size: 18px;
}

.light {
  margin: 20px;
  border: 1px solid #000;
}

#red {
  height: 100px;
  width: 100px;
  background: #E53A40;
  opacity: 0.1;
}

#yellow {
  height: 100px;
  width: 100px;
  background: #EFDC05;
  opacity: 0.1;
}

#green {
  height: 100px;
  width: 100px;
  background: #75D701;
  opacity: 0.1;
}

#blue {
  height: 100px;
  width: 100px;
  background: #30A9DE;
  opacity: 0.1;
}

.active {
  opacity: 1.0 !important;
}



</style>


