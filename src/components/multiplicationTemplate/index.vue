<template>
  <div id="main" :class="{green: correct, red: !correct}">
      <div id="content">
          <p id="nomeration">{{ index }}</p>
          <slot id="timer" name="timer"></slot>
          <p>{{ number1 }} X {{ number2 }} =</p>
          <input @keyup.enter="check" ref='inputField' type="number" v-model="enteredNumber">
          <button id="btns" class="btn btn-primary" @click="check">Submit</button>
      </div>
  </div>
</template>

<script>
export default {
    name: "MultiplicationTemplate",
    props: ['count', 'addComponent', 'start', 'stop', 'stopTimerExistance', 'index', 'limitOfTen', 'component'],
    data() {
        return {
            number1: Math.floor(Math.random() * 10),
            number2: Math.floor(Math.random() * 10),
            enteredNumber: undefined,
            result: undefined,
            correct: false,
            executed: false
        }
    },
    methods: {
        randomFunction() {
            const num1Random = Math.floor(Math.random()*10);
            this.number1 = num1Random;
            const num2Random = Math.floor(Math.random()*10);
            this.number2 = num2Random;
            console.log(this.number1, this.number2);
            
        },
        check() {
            if (this.executed == false) {
                const calcResult = this.number1 * this.number2;
                if (this.enteredNumber == calcResult) {
                    this.correct = true;
                    if (this.stopTimerExistance == true) {
                        this.stop();
                    }
                    this.executed = true;

                    if (this.component == 'InfiniteGame') {
                        this.addComponent();
                    } else if (this.component == 'TrackGame') {
                        this.limitOfTen();
                    }
                } else {
                    this.correct = false;
                }

            }
            
            
        },
        focused() {
            this.$refs.inputField.focus();
        },
        
    },
    computed: {
        colorful() {
            return {
                backgroundColor: this
            }
        }
    },
    mounted() {
        this.focused();
    }
}
</script>

<style>

#main {
    width: 600px;
    height: 110px;
    margin-left: auto;
    margin-right: auto;
    display:inline-block;
    border-radius: 15px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

#content {
    margin-top: 35px;
    font-size: 25px;
}

p {
    display:inline-block;
    padding: 0px;
    margin: 0px;
    margin-right: 10px;
}

#nomeration {
    background-color: white;
    border-radius: 200px;
    padding: 0 10px 0 10px;
    float: left;
    margin-left: 60px;
    margin-right: -30px;
}

input {
    display:inline-block;
    height: 28px;
    font-size: 25px;
    width: 100px; 
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

#btns {
    margin-left: 30px;
}

.red {
    background-color: red;
}

.green {
    background-color: greenyellow;
}
</style>