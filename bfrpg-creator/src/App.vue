<template>
  <div id="app">
    <h1>Basic Fantasy RPG Character Creator</h1>

    <h3>Choose Your Race</h3>

    <!--     <b-card no-body class="mb-1" v-on:click="character.race = 'human'">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block href="#" v-b-toggle.accordion-1 variant="info">Human</b-button>
      </b-card-header>
      <b-collapse id="accordion-1" visible accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <table class="table table-striped">
              <tbody>
                <tr>
                  <td class="font-weight-bold">Ability Requirements</td>
                  <td class="text-left">none</td>
                </tr>
                <tr>
                  <td class="font-weight-bold">Classes</td>
                  <td class="text-left">Any</td>
                </tr>
                <tr>
                  <td class="font-weight-bold">Hit Die</td>
                  <td class="text-left">Based on class</td>
                </tr>
              </tbody>
            </table>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>

    <b-card no-body class="mb-1" v-on:click="character.race = 'elf'">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block href="#" v-b-toggle.accordion-2 variant="info">Elf</b-button>
      </b-card-header>
      <b-collapse id="accordion-2" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>{{ character.race }}</b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>

    <b-card no-body class="mb-1" v-on:click="character.race = 'dwarf'">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button
          block
          href="#"
          v-b-toggle.accordion-3
          variant="info"
          v-on:click="counter += 1"
        >Dwarf</b-button>
      </b-card-header>
      <b-collapse id="accordion-3" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>{{ counter }}</b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>

    <b-card no-body class="mb-1" v-on:click="character.race = 'halfling'">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block href="#" v-b-toggle.accordion-3 variant="info">Halfling</b-button>
      </b-card-header>
      <b-collapse id="accordion-3" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>{{ text }}</b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>-->

    <b-form-group>
      <b-form-radio-group
        id="btn-radios-2"
        buttons
        name="radio-btn-outline"
        button-variant="outline-primary"
        size="lg"
      >
        <b-button v-on:click="changeRace(races.human)">HUMAN</b-button>
        <b-button v-on:click="changeRace(races.elf)">ELF</b-button>
        <b-button v-on:click="changeRace(races.dwarf)">DWARF</b-button>
        <b-button v-on:click="changeRace(races.halfling)">HALFLING</b-button>
      </b-form-radio-group>
    </b-form-group>

    <table class="table table-striped" v-if="character.race != ''">
      <tbody>
        <tr>
          <td class="font-weight-bold text-right" style="width: 50%">Ability Requirements</td>
          <td class="text-left" role="cell">{{raceattributes.ar}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Classes</td>
          <td class="text-left">{{raceattributes.class}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Hit Die</td>
          <td class="text-left">{{raceattributes.hd}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Weapons</td>
          <td class="text-left">{{raceattributes.weapons}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Special</td>
          <td class="text-left">{{raceattributes.special}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Save Bonuses</td>
          <td class="text-left">{{raceattributes.save}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Languages</td>
          <td class="text-left">{{raceattributes.lang}}</td>
        </tr>
        <tr>
          <td class="font-weight-bold text-right">Description</td>
          <td class="text-left">{{raceattributes.desc}}</td>
        </tr>
      </tbody>
    </table>

    <div v-if="character.race != ''">
      <h3>Choose a class</h3>
        <b-form-group>
      <b-form-radio-group
        id="btn-radios-2"
        buttons
        name="radio-btn-outline"
        button-variant="outline-primary"
        size="lg"
      >
        <b-button v-on:click="changeRace(races.human)">FIGHTER</b-button>
        <b-button v-on:click="changeRace(races.elf)">CLERIC</b-button>
        <b-button v-if="character.race != races.dwarf && character.race != races.halfling" v-on:click="changeRace(races.dwarf)">MAGIC-USER</b-button>
        <b-button v-on:click="changeRace(races.halfling)">THIEF</b-button>
        <b-button v-if="character.race == races.elf" v-on:click="changeRace(races.halfling)">FIGHTER/MAGE</b-button>
        <b-button v-if="character.race == races.elf" v-on:click="changeRace(races.halfling)">MAGE/THIEF</b-button>
      </b-form-radio-group>
    </b-form-group>
    </div>

    <div
      id="floatingChoices"
      class="fixed-top"
    >RACE : {{character.race}} | CLASS : {{character.class}} | LEVEL : {{character.level}}</div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      races: {
        none: "",
        human: "human",
        elf: "elf",
        dwarf: "dwarf",
        halfling: "halfling"
      },
      character: {
        race: "",
        class: "",
        name: "",
        level: 1,
        attackbonus: "",
        hitDice: 4,
        saves: {
          deathray: ""
        }
      },
      raceattributes: {
        ar: "",
        class: "",
        hd: "",
        weapons: "",
        special: "",
        save: "",
        lang: "",
        desc: ""
      }
    };
  },
  methods: {
    changeRace: function(race) {
      this.character.race = race;

      switch (race) {
        case "human":
          this.raceattributes.ar = "None";
          this.raceattributes.class = "Any";
          this.raceattributes.hd = "Any-based on class";
          this.raceattributes.weapons = "Large weapons require 2 hands";
          this.raceattributes.special = "+1-% on all earned experience";
          this.raceattributes.save = "None";
          this.raceattributes.lang = "Common, +1 per INT bonus";
          this.raceattributes.desc =
            "Average male is typically 6' tall, 175 lbs., and lives about 75 years";
          break;
        case "elf":
          this.raceattributes.ar = "INT 9 or higher, CON 17 or lower";
          this.raceattributes.class =
            "Any single as well as Fighter/Magic-User and Magic-User/Thief";
          this.raceattributes.hd = "d6 max";
          this.raceattributes.weapons = "Large weapons require 2 hands";
          this.raceattributes.special =
            "Darkvision (60' range), Detect secret doors (1-2 on D6, 1 on cursory), Immune to paralyzing touch of ghouls";
          this.raceattributes.save =
            "+2 vs. Magic Wands, +1 vs. Paralysis or Petrify, +2 vs. Spells";
          this.raceattributes.lang = "Common, Elvish, +1 per INT bonus";
          this.raceattributes.desc =
            "Typically about 5' tall, slender, 130 lbs, lives about 1200 years or more";
          break;
        case "dwarf":
          this.raceattributes.ar = "CON 9 or higher, CHA 17 or lower";
          this.raceattributes.class = "Cleric, Fighter, Thief";
          this.raceattributes.hd = "Any";
          this.raceattributes.weapons =
            "Large weapons require 2 hands, No 2-handed swords, pole-arms or longbows";
          this.raceattributes.special =
            "Darkvision (60' range), Detect new construction, shifting walls, slanting passages, traps with (1-2 on D6)";
          this.raceattributes.save =
            "+4 vs. Death Ray or Poison, +4 vs. Magic Wands, +4 vs. Paralysis or Petrify, +3 vs. Dragon Breath, +4 vs. Spells";
          this.raceattributes.lang = "Common, Dwarvish, +1 per INT bonus";
          this.raceattributes.desc =
            "Typically about 4' tall, stocky, lifespan of 300-400 years.  Thick hair and beards";
          break;
        case "halfling":
          this.raceattributes.ar = "DEX 8 or higher, STR 17 or lower";
          this.raceattributes.class = "leric, Fighter, Thief";
          this.raceattributes.hd = "d6 max";
          this.raceattributes.weapons =
            "Must use medium weapons in two hands, cannot use large weapons";
          this.raceattributes.special =
            "+1 attack bonus on ranged weapons, +2 bonus to AC when attacked in melee by creatures larger than man-sized, +1 to initiative rolls, Hide ability (10% detection outdoors, 30% detection indoors)";
          this.raceattributes.save =
            "+4 vs. Death Ray or Poison, +4 vs. Magic Wands, +4 vs. Paralysis or Petrify, +3 vs. Dragon Breath, +4 vs. Spells";
          this.raceattributes.lang = "Common, Halfling, +1 per INT bonus";
          this.raceattributes.desc =
            "Typically 3ft tall, 60lbs, curly hair and no facial hair, lifespan about 100 years";
          break;
      }
    }
  }
};

const Race = Object.freeze({
  NONE: "",
  HUMAN: "human",
  ELF: "elf",
  DWARF: "dwarf",
  HALFLING: "halfling"
});
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
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
</style>
