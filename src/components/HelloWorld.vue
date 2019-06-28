<template>
  <div class="hello">

    <div class="row justify-center">
      <div class="col-4 ">
        <h3> YOU </h3>
      </div>
      <div class="col-1">

      </div>
      <div class="col-4">
        <h3> MONSTER </h3>
      </div>
    </div>

    <div class="row justify-center">
      <div class="col-4" >
        <h5 class="bar">
          <p :style="{ width: playerHp + '%', backgroundColor: color }">
            {{ playerHp }}
          </p>
        </h5>
      </div>
      <div class="col-1">

      </div>
      <div class="col-4">
        <h5 class="bar">
          <p :style="{ width: monsterHp + '%', backgroundColor: color }">
            {{ monsterHp }}
          </p>
        </h5>
      </div>
    </div>

    <div v-if="!start" class="row justify-center">
      <div class="col-10 shadow-4">
        <div class="grid-space">
          <q-btn @click="start=!start" color="white" text-color="black" label="Start New Game" />
        </div>
      </div>
    </div>

    <div v-if="start" class="row justify-center">
        <div class="col-10 shadow-4">
          <div class="q-gutter-x-xl grid-space">
            <q-btn @click="onAttack" color="red" text-color="black" label="Attack" />
            <q-btn @click="onSpecial" color="orange" text-color="black" label="Special Attack" />
            <q-btn @click="onHeal" color="green" text-color="black" label="Heal" />
            <q-btn @click="start=!start, play=false" color="white" text-color="black" label="Give Up" />
          </div>
        </div>
    </div>

      <div v-if="prints.length > 0" class="row justify-center" style="margin-top: 30px">
        <div class="col-10 shadow-4">
          <div class="grid-space">
          <div class="col-4" :class= print.classStyle v-for="print in prints" :key="print.index">
            {{ print.text }}
          </div>
          </div>
        </div>
      </div>



  </div>
</template>

<script>
export default {
    name: 'HelloWorld',

    data() {
        return {
            start: false,
            playerHp: 100,
            monsterHp: 100,
            hp: 100,
            mAttackMsg: "Monster attacks player for ",
            yAttackMsg: "Player attacks Monster for ",
            yHealMsg: "Player heals for ",
            ySAttackMsg: "Player special attacks monster for ",
            prints: [],
            color: 'mediumseagreen'
        }

    },

    methods: {

        random(value){
            return Math.floor(Math.random()* value) ;
        },

        onAttack() {
            let yourRandom = this.random(20);
            let monsterRandom = this.random(10);
            this.playerHp -= yourRandom;
            this.monsterHp -= monsterRandom;
            this.prints.unshift({
                text: this.mAttackMsg + yourRandom,
                classStyle: 'you'
            });

            this.prints.unshift({
                text: this.yAttackMsg + monsterRandom,
                classStyle: 'monster'
            });
            this.result()
        },

        onSpecial() {
            let yourRandom = this.random(20);
            let monsterRandom = this.random(30);
            this.playerHp -= yourRandom;
            this.monsterHp -= monsterRandom;
            this.prints.unshift({
                text: this.mAttackMsg + yourRandom,
                classStyle: 'you'
            });

            this.prints.unshift({
                text: this.ySAttackMsg + monsterRandom,
                classStyle: 'monster'
            })
            this.result()
        },
        onHeal() {
            let yourRandom = this.random(20);
            let healRandom = this.random(20);
            if(this.playerHp <= 90){
                this.playerHp += healRandom;
            }
            else{
                this.playerHp = 100;
            }
            this.playerHp -= yourRandom;
            this.prints.unshift({
                text: this.mAttackMsg + yourRandom,
                classStyle: 'you'
            });

            this.prints.unshift({
                text: this.yHealMsg + healRandom,
                classStyle: 'monster'
            });
            this.result()
        },

        result() {

            if(this.playerHp <= 0){
                alert('You lose');
                this.start = false;
                this.playerHp = 100;
                this.monsterHp = 100;
                this.prints = [];
            }

            if(this.monsterHp <= 0){
                alert('You win');
                this.start = false;
                this.playerHp = 100;
                this.monsterHp = 100;
                this.prints = [];
            }


        }
    }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  h3 {
    font-size: 40px;
    display: inline-block;
  }

  h5{
    margin-top: 0px;
    background-color: lightgray;
    color: white;
  }

  .grid-space {
    margin: 2% 5%;
  }

  .you {
    background-color: pink;
    margin-bottom: 1%
  }

  .monster {
    background-color: lightskyblue;
    margin-bottom: 1%
  }


</style>
