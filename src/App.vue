

<template>

  <div id="headline">
    <h1 class="red">MONSTER SLAYER</h1>
    <h2></h2>
    <div id="playersimg" style="margin-top: 50px;">
      <div><img v-if="player.status == 'alive'" style="width: auto; height: 200px;" src="@/assets/freeman.png"></div>
      <div><img v-if="monster.status == 'alive'" style="width: auto; height: 200px;" src="@/assets/monster.png"></div>
    </div>
  </div>

  <div id="health">

    <div id="statusbox" v-if="player.status == 'dead' || monster.status == 'dead'">
      <h2 class="red" v-if="player.status == 'dead'"> {{ player.name }} has died! <button @click="newround" class="primbutton">start over</button></h2>
      <h2 class="red" v-if="monster.status == 'dead'">{{ monster.name }} has died! <button @click="newround" class="primbutton">continue</button></h2>
    </div>

    <div v-if="player.status == 'alive' && monster.status == 'alive'" class="containerbox">
      <h2 style="margin-top: 10px;">Player Health: {{ playerhealth }}</h2>
      <input class="healthbar" type="range" min="0" max="100" :value="player.health">

      <h2 style="margin-top: 20px;">Monster Health: {{ monsterhealth }}</h2>
      <input class="healthbar" type="range" min="0" max="100" :value="monster.health">
    </div>

    <div v-if="player.status == 'alive' && monster.status == 'alive'" class="containerbox">

      <div v-if="!blocking" class="contolgrid">
        <div class="controlbox"><button @click="attack1()" class="primbutton">Attack1</button></div>
        
        <div class="controlbox"><button @click="attack2()" class="primbutton">Attack2</button></div>
        <div class="controlbox"><button @click="attack3()" class="primbutton">Attack3</button></div>
        <div class="controlbox"><button @click="heal()" class="primbutton">Heal</button></div>
      </div>
      <div>
        <h2 class="red" v-if="blocking">{{ currentmove }}</h2>
      </div>
    </div>

  </div>

</template>


<script>

  export default 
  {
    data()
    {
      return {
        blocking: false,
        currentmove: '',
        player: {
          health: 100,
          name: 'Freeman',
          status: 'alive'
        },
        monster: {
          health: 100,
          name: 'Monster',
          status: 'alive'
        }
      }
    },
    computed: 
    {
      // Computed
    },
    watch: 
    {
        'player.health': function (newValue, oldValue) {
          if (newValue <= 0) {
            this.player.status = 'dead';
          }
        },
        'monster.health': function (newValue, oldValue) {
          if (newValue <= 0) {
            this.monster.status = 'dead';
          }
        }
    },
    methods:
    {
      attack1()
      {
        if (this.blocking) return // exit method if attack is still being cooled down
        // perform attack logic here

        this.currentmove = 'Attack1';

        let dmg = Math.floor(Math.random() * (20 - 5 + 1)) + 5;
        this.monster.health -= dmg;

        if(this.monster.health <= 0)
        {
          this.monster.status = 'dead';
          return;
        }

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
          this.monsterattacks();
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      attack2()
      {
        if (this.blocking) return // exit method if attack is still being cooled down
        // perform attack logic here

        this.currentmove = 'Attack2';

        let dmg = Math.floor(Math.random() * (40 - 5 + 1)) + 5;
        this.monster.health -= dmg;

        if(this.monster.health <= 0)
        {
          this.monster.status = 'dead';
          return;
        }

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
          this.monsterattacks2();
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      attack3()
      {
        if (this.blocking) return // exit method if attack is still being cooled down
        // perform attack logic here

        this.currentmove = 'Attack3';

        let dmg = Math.floor(Math.random() * (30 - 5 + 1)) + 5;
        this.monster.health -= dmg;

        if(this.monster.health <= 0)
        {
          this.monster.status = 'dead';
          return;
        }

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
          this.monsterattacks3();
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      heal()
      {
        if (this.blocking) return // exit method if attack is still being cooled down
        // perform attack logic here

        this.currentmove = 'healing';

        let heal = 10;
        this.player.health += heal;


        if(this.player.health >= 100)
        {
          this.player.health = 100;
        }

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
          this.monsterattacks();
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      monsterattacks()
      {
        this.currentmove = 'Monster Attacks';

        let dmg = Math.floor(Math.random() * (20 - 5 + 1)) + 5;
        this.player.health -= dmg;

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      monsterattacks2()
      {
        this.currentmove = 'Monster Attacks';

        let dmg = Math.floor(Math.random() * (60 - 5 + 1)) + 5;
        this.player.health -= dmg;

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      monsterattacks3()
      {
        this.currentmove = 'Monster Attacks';

        let dmg = Math.floor(Math.random() * (25 - 5 + 1)) + 5;
        this.player.health -= dmg;

        this.blocking = true // set blocking flag to true
        setTimeout(function() {
          this.blocking = false // reset blocking flag after 1 second (1000 milliseconds)
        }.bind(this), 1000) // bind `this` to reference Vue instance inside setTimeout 

      },
      newround()
      {
        this.player.health = 100;
        this.player.status = 'alive';
        this.monster.health = 100;
        this.monster.status = 'alive';
      }
    }
  }

</script>

<style>
#headline
{
  text-align: center;
  padding-top: 50px;
  padding-bottom: 50px;
}

.red
{
  color: red;
}

.containerbox
{
  max-width: 400px;
  text-align: center;
  width: 100%;
  margin: 20px auto;
  background-color: #eee;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.26);
}

#statusbox
{
  max-width: 400px;
  text-align: center;
  width: 100%;
  margin: 20px auto;
  background-color: #eee;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.26);
}

input[type="range"] {
  -webkit-appearance: none;
  width: 100%;
  height: 14px;
  border-radius: 7px;
  background: orange;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

input[type="range"]:hover {
  opacity: 1;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 10px;
  background: blue;
  cursor: pointer;
}

input[type="range"]::-moz-range-thumb {
  width: 20px;
  height: 20px;
  border-radius: 10px;
  background: blue;
  cursor: pointer;
}

.contolgrid
{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 10px;
  justify-content: center;
}

.controlbox
{
  max-width: 180px;
  width: 100%;
}

@media only screen and (max-width: 600px) 
{
  .contolgrid
  {
    grid-template-columns: 1fr;
  }
  .controlbox
  {
    max-width: 100%;
    width: 100%;
  }
}


.primbutton
{
  width: 100%;
  background-color: blue;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.26);
  transition: all 0.3s ease;
}

.primbutton:hover
{
  background-color: red;
}


#playersimg
{
  max-width: 400px;
  margin-left: auto;
  margin-right: auto;
  display: flex;
  justify-content: space-between;
}
</style>
