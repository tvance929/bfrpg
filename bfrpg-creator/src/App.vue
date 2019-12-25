<template>
  <div id="app">
    <div
      id="floatingChoices"
      class="fixed-top border border-secondary rounded floatingheader"
    >RACE : {{character.race}} | CLASS : {{character.class}} | LEVEL : {{character.level}}</div>
    <h1>Basic Fantasy RPG Character Creator</h1>

    <div class="border border-secondary rounded onepercent" v-if="currentsection == sections.RACE">
      <h3>Choose Your Race</h3>
      <b-form-group>
        <b-form-radio-group
          id="btn-radios-2"
          buttons
          name="radio-btn-outline"
          button-variant="outline-primary"
          size="lg"
        >
          <b-button v-on:click="setRace(races.HUMAN)">HUMAN</b-button>
          <b-button v-on:click="setRace(races.ELF)">ELF</b-button>
          <b-button v-on:click="setRace(races.DWARF)">DWARF</b-button>
          <b-button v-on:click="setRace(races.HALFLING)">HALFLING</b-button>
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
    </div>

    <div
      class="border border-secondary rounded onepercent"
      v-if="currentsection == sections.ABILITIES"
    >
      <h3>Set Ability Scores</h3>
      <span>
        Roll 3 D6 for each ability OR use the option of a Standard Array ( 15, 14, 13, 10, 8).
        <br />*You can add +1 to any score if you take a -2 from other scores, going to 18 will cost you -3 points.
      </span>
      <b-container fluid>
        <b-row class="my-1">
          <b-col>
            <b-container fluid class="onepercent" id="diceRoller">
              <b-row class="my-1">
                <b-col sm="2">
                  <b-button
                    variant="primary"
                    v-if="currentsection != sections.CLASS"
                    v-on:click="rollForAbility()"
                  >ROLL DICE</b-button>
                </b-col>
                <b-col>
                  <span>{{randomroll.one}}</span>
                </b-col>
                <b-col>
                  <span>{{randomroll.two}}</span>
                </b-col>
                <b-col>
                  <span>{{randomroll.three}}</span>
                </b-col>
                <b-col>
                  <span>{{randomroll.total}}</span>
                </b-col>
              </b-row>
            </b-container>
            <b-container fluid class="onepercent">
              <b-row class="my-1">
                <b-col sm="2">
                  <label for="input-large">Strength:</label>
                </b-col>
                <b-col sm="10">
                  <b-form-input
                    id="abilityInputStrength"
                    size="lg"
                    placeholder="raw physical power"
                    v-model.number="character.abilities.strength"
                    @blur.native="checkAbilityScore(abilities.STRENGTH)"
                    :state="abilityerrors.strengtherror == '' ? (character.abilities.strength == '' ? null : true) : false"
                    type="number"
                    min="3"
                    max="18"
                  ></b-form-input>
                  <span>{{abilityerrors.strengtherror}}</span>
                </b-col>
              </b-row>
              <b-row class="my-1">
                <b-col sm="2">
                  <label for="input-large">Dexterity:</label>
                </b-col>
                <b-col sm="10">
                  <b-form-input
                    id="abilityInputDexterity"
                    size="lg"
                    placeholder="quickness, balance, aptitude with tools"
                    v-model.number="character.abilities.dexterity"
                    @blur.native="checkAbilityScore(abilities.DEXTERITY)"
                    :state="abilityerrors.dexterityerror == '' ? (character.abilities.dexterity == '' ? null : true) : false"
                    type="number"
                    min="3"
                    max="18"
                  ></b-form-input>
                  <span>{{abilityerrors.dexterityerror}}</span>
                </b-col>
              </b-row>
              <b-row class="my-1">
                <b-col sm="2">
                  <label for="input-large">Intelligence:</label>
                </b-col>
                <b-col sm="10">
                  <b-form-input
                    id="abilityInputIntelligence"
                    size="lg"
                    placeholder="ability to learn and apply knowledge"
                    v-model.number="character.abilities.intelligence"
                    @blur.native="checkAbilityScore(abilities.INTELLIGENCE)"
                    :state="abilityerrors.intelligenceerror == '' ? (character.abilities.intelligence == '' ? null : true) : false"
                    type="number"
                    min="3"
                    max="18"
                  ></b-form-input>
                  <span>{{abilityerrors.intelligenceerror}}</span>
                </b-col>
              </b-row>
              <b-row class="my-1">
                <b-col sm="2">
                  <label for="input-large">Wisdom:</label>
                </b-col>
                <b-col sm="10">
                  <b-form-input
                    id="abilityInputWisdom"
                    size="lg"
                    placeholder="intuition, willpower, common sense"
                    v-model.number="character.abilities.wisdom"
                    @blur.native="checkAbilityScore(abilities.WISDOM)"
                    :state="abilityerrors.wisdomerror == '' ? (character.abilities.wisdom == '' ? null : true) : false"
                    type="number"
                    min="3"
                    max="18"
                  ></b-form-input>
                  <span>{{abilityerrors.wisdomerror}}</span>
                </b-col>
              </b-row>
              <b-row class="my-1">
                <b-col sm="2">
                  <label for="input-large">Constitution:</label>
                </b-col>
                <b-col sm="10">
                  <b-form-input
                    id="abilityInputConstitution"
                    size="lg"
                    placeholder="general health and vitality"
                    v-model.number="character.abilities.constitution"
                    @blur.native="checkAbilityScore(abilities.CONSTITUTION)"
                    :state="abilityerrors.constitutionerror == '' ? (character.abilities.constitution == '' ? null : true) : false"
                    type="number"
                    min="3"
                    max="18"
                  ></b-form-input>
                  <span>{{abilityerrors.constitutionerror}}</span>
                </b-col>
              </b-row>
              <b-row class="my-1">
                <b-col sm="2">
                  <label for="input-large">Charisma:</label>
                </b-col>
                <b-col sm="10">
                  <b-form-input
                    id="abilityInputCharisma"
                    size="lg"
                    placeholder=" ability to influence, lead people"
                    v-model.number="character.abilities.charisma"
                    @blur.native="checkAbilityScore(abilities.CHARISMA)"
                    :state="abilityerrors.charismaerror == '' ? (character.abilities.charisma == '' ? null : true) : false"
                    type="number"
                    min="3"
                    max="18"
                  ></b-form-input>
                  <span>{{abilityerrors.charismaerror}}</span>
                </b-col>
              </b-row>
            </b-container>
          </b-col>
        </b-row>
      </b-container>
      <span></span>
    </div>

    <div v-show="false">
      <h3>Choose a class</h3>
      <b-form-group>
        <b-form-radio-group
          id="btn-radios-2"
          buttons
          name="radio-btn-outline"
          button-variant="outline-primary"
          size="lg"
        >
          <b-button v-on:click="setClass(classes.FIGHTER)">FIGHTER</b-button>
          <b-button v-on:click="setClass(classes.CLERIC)">CLERIC</b-button>
          <b-button
            v-if="character.race != races.DWARF && character.race != races.HALFLING"
            v-on:click="setClass(classes.MAGICUSER)"
          >MAGIC-USER</b-button>
          <b-button v-on:click="setClass(classes.THIEF)">THIEF</b-button>
          <b-button
            v-if="character.race == races.ELF"
            v-on:click="setClass(classes.halfling)"
          >FIGHTER/MAGE</b-button>
          <b-button
            v-if="character.race == races.ELF"
            v-on:click="setClass(classes.halfling)"
          >MAGE/THIEF</b-button>
        </b-form-radio-group>
      </b-form-group>
    </div>

    <b-container fluid class="onepercent" v-if="character.race != ''">
      <b-row>
        <b-col>
          <b-button
            variant="primary"
            size="lg"
            v-if="currentsection != sections.RACE"
            v-on:click="changeSection('prev')"
          >PREV</b-button>
        </b-col>
        <b-col>
          <b-button
            variant="primary"
            size="lg"
            v-if="currentsection != sections.CLASS"
            v-on:click="changeSection('next')"
          >NEXT</b-button>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      character: {
        race: "",
        class: "",
        name: "",
        level: 1,
        attackbonus: "",
        hitDice: 4,
        abilities: {
          strength: "",
          dexterity: "",
          intelligence: "",
          wisdom: "",
          constitution: "",
          charisma: ""
        },
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
      },
      currentsection: "race",
      races: {
        none: "",
        HUMAN: "human",
        ELF: "elf",
        DWARF: "dwarf",
        HALFLING: "halfling"
      },
      classes: {
        NONE: "",
        FIGHTER: "Fighter",
        CLERIC: "Cleric",
        MAGICUSER: "Magic-User",
        THIEF: "Thief"
      },
      abilities: {
        STRENGTH: "strength",
        INTELLIGENCE: "intelligence",
        WISDOM: "wisdom",
        DEXTERITY: "dexterity",
        CONSTITUTION: "constitution",
        CHARISMA: "charisma"
      },
      sections: {
        RACE: "race",
        ABILITIES: "abilities",
        CLASS: "class"
      },
      randomroll: {
        one: 0,
        two: 0,
        three: 0,
        total: 0
      },
      abilityerrors: {
        strengtherror: "",
        dexterityerror: "",
        constitutionerror: "",
        charismaerror: "",
        intelligenceerror: "",
        wisdomerror: ""
      }
    };
  },
  methods: {
    setRace: function(race) {
      this.character.race = race;

      switch (race) {
        case this.races.HUMAN:
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
        case this.races.ELF:
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
        case this.races.DWARF:
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
        case this.races.HALFLING:
          this.raceattributes.ar = "DEX 8 or higher, STR 17 or lower";
          this.raceattributes.class = "Cleric, Fighter, Thief";
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
      //Reset everything else
      this.character.abilities.strength = "";
      this.character.abilities.dexterity = "";
      this.character.abilities.intelligence = "";
      this.character.abilities.wisdom = "";
      this.character.abilities.constitution = "";
      this.character.abilities.charisma = "";
      this.abilityerrors.strengtherror = "";
      this.abilityerrors.dexterityerror = "";
      this.abilityerrors.intelligenceerror = "";
      this.abilityerrors.wisdomerror = "";
      this.abilityerrors.constitutionerror = "";
      this.abilityerrors.charismaerror = "";
      this.character.class = "";
    },
    setClass: function(classname) {
      this.character.class = classname;
    },
    changeSection: function(prevOrNext) {
      if (prevOrNext == "next") {
        switch (this.currentsection) {
          case this.sections.RACE:
            this.currentsection = this.sections.ABILITIES;
            break;
        }
      } else {
        switch (this.currentsection) {
          case this.sections.ABILITIES:
            this.currentsection = this.sections.RACE;
            break;
        }
      }
    },
    rollForAbility: function() {
      this.randomroll.one = Math.floor(Math.random() * 6 + 1);
      this.randomroll.two = Math.floor(Math.random() * 6 + 1);
      this.randomroll.three = Math.floor(Math.random() * 6 + 1);
      this.randomroll.total =
        this.randomroll.one + this.randomroll.two + this.randomroll.three;
    },
    checkAbilityScore: function(ability) {
      switch (ability) {
        case this.abilities.STRENGTH:
          var str = this.character.abilities.strength;
          if (str == "") {
            this.abilityerrors.strengtherror = "";
            return;
          } else if (str >= 18) {
            this.character.abilities.strength = 18;
            if (this.character.race == this.races.HALFLING) {
              this.abilityerrors.strengtherror =
                "Halflings cannot have 18 strength.";
              return;
            }
          } else if (str < 3) {
            this.character.abilities.strength = 3;
          }
          this.abilityerrors.strengtherror = "";
          break;
        case this.abilities.INTELLIGENCE:
          var int = this.character.abilities.intelligence;
          if (int == "") {
            this.abilityerrors.intelligenceerror = "";
            return;
          } else if (int >= 18) {
            this.character.abilities.intelligence = 18;
          } else if (int < 9) {
            if (int < 3) {
              this.character.abilities.intelligence = 3;
            }
            if (this.character.race == this.races.ELF) {
              this.abilityerrors.intelligenceerror =
                "Elves cannot have Intelligence less than 9";
              return;
            }
          }
          this.abilityerrors.intelligenceerror = "";
          break;
        case this.abilities.WISDOM:
          var wis = this.character.abilities.wisdom;
          if (wis == "") {
            this.abilityerrors.wisdomerror = "";
            return;
          } else if (wis >= 18) {
            this.character.abilities.wisdom = 18;
          } else if (wis < 3) {
            this.character.abilities.wisdom = 3;
          }
          this.abilityerrors.wisdomerror = "";
          break;
        case this.abilities.DEXTERITY:
          var dex = this.character.abilities.dexterity;
          if (dex == "") {
            this.abilityerrors.dexterityerror = "";
            return;
          } else if (dex >= 18) {
            this.character.abilities.dexterity = 18;
          } else if (dex < 8) {
            if (dex < 3) {
              this.character.abilities.dexterity = 3;
            }
            if (this.character.race == this.races.HALFLING) {
              this.abilityerrors.dexterityerror =
                "Halflings cannot have a dexterity below 8.";
              return;
            }
          }
          this.abilityerrors.dexterityerror = "";
          break;
        case this.abilities.CONSTITUTION:
          var con = this.character.abilities.constitution;
          if (con == "") {
            this.abilityerrors.constitutionerror = "";
            return;
          } else if (con >= 18) {
            this.character.abilities.constitution = 18;
            if (this.character.race == this.races.ELF) {
              this.abilityerrors.constitutionerror =
                "Elves cannot have a constitution higher than 17.";
              return;
            }
          } else if (con < 9) {
            if (con < 3) {
              this.character.abilities.constitution = 3;
            }
            if (this.character.race == this.races.DWARF) {
              this.abilityerrors.constitutionerror =
                "Dwarves cannot have a constitution below 9.";
              return;
            }
          }
          this.abilityerrors.constitutionerror = "";
          break;
        case this.abilities.CHARISMA:
          var cha = this.character.abilities.charisma;
          if (cha == "") {
            this.abilityerrors.constitutionerror = "";
            return;
          } else if (cha >= 18) {
            this.character.abilities.charisma = 18;
            if (this.character.race == this.races.DWARF) {
              this.abilityerrors.charismaerror =
                "Dwarves cannot have a charisma higher than 17.";
              return;
            }
          } else if (cha < 3) {
            this.character.abilities.constitution = 3;
          }
          this.abilityerrors.constitutionerror = "";
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

.onepercent {
  margin: 1%;
}

.floatingheader {
  padding: 1%;
  background-color: white;
}
</style>
