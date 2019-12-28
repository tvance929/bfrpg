<template>
  <div id="app">
    <div>
      <b-button v-b-toggle.collapse-1 variant="primary" class="fixed-top right">Character Sheet</b-button>
      <b-collapse id="collapse-1" class="mt-2">
        <b-card
          class="border border-secondary rounded floatingheader onepercent text-left charSheet"
        >
          <b-container fluid style="charSheet">
            <b-row class="my-1 pb-4">
              <b-col>
                <span class="font-weight-bolder">NAME:</span>
                <span
                  class="text-capitalize sheetField editable"
                  contenteditable="true"
                >{{character.name}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">PLAYER:</span>
                <span
                  class="text-capitalize sheetField editable"
                  contenteditable="true"
                >{{character.player}}</span>
              </b-col>
            </b-row>
            <b-row class="my-1 pb-4">
              <b-col>
                <span class="font-weight-bolder">RACE:</span>
                <span class="text-capitalize sheetField">{{character.race}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">CLASS:</span>
                <span class="text-capitalize sheetField">{{character.class}}</span>
              </b-col>
            </b-row>
            <b-row class="my-1 pb-4">
              <b-col>
                <span class="font-weight-bolder">LEVEL:</span>
                <span class="text-capitalize sheetSmallField">{{character.level}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">XP:</span>
                <span class="text-capitalize sheetSmallField">{{character.xp}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">SEX:</span>
                <span class="text-capitalize sheetField">
                  <b-form-select v-model="character.sex">
                    <option value="Male" selected="true">Male</option>
                    <option value="Female">Female</option>
                  </b-form-select>
                </span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">AGE:</span>
                <span
                  class="text-capitalize sheetSmallField editable"
                  contenteditable="true"
                >{{character.age}}</span>
              </b-col>
            </b-row>
            <b-row class="my-1 pb-4">
              <b-col>
                <span class="font-weight-bolder abilityName">STR:</span>
                <span
                  class="text-capitalize sheetSmallField"
                >{{character.abilities.strength}} {{character.abilities.strength != "" ? abilityBonus(character.abilities.strength) : ""}}</span>
                <br />
                <span class="font-weight-bolder abilityName">INT:</span>
                <span
                  class="text-capitalize sheetSmallField"
                >{{character.abilities.intelligence}} {{character.abilities.intelligence != "" ? abilityBonus(character.abilities.intelligence) : ""}}</span>
                <br />
                <span class="font-weight-bolder abilityName">WIS:</span>
                <span
                  class="text-capitalize sheetSmallField"
                >{{character.abilities.wisdom}} {{character.abilities.wisdom != "" ? abilityBonus(character.abilities.wisdom) : ""}}</span>
                <br />
                <span class="font-weight-bolder abilityName">DEX:</span>
                <span
                  class="text-capitalize sheetSmallField"
                >{{character.abilities.dexterity}} {{character.abilities.dexterity != "" ? abilityBonus(character.abilities.dexterity) : ""}}</span>
                <br />
                <span class="font-weight-bolder abilityName">CON:</span>
                <span
                  class="text-capitalize sheetSmallField"
                >{{character.abilities.constitution}} {{character.abilities.constitution != "" ? abilityBonus(character.abilities.constitution) : ""}}</span>
                <br />
                <span class="font-weight-bolder abilityName">CHA:</span>
                <span
                  class="text-capitalize sheetSmallField"
                >{{character.abilities.charisma}} {{character.abilities.charisma != "" ? abilityBonus(character.abilities.charisma) : ""}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">AC:</span>
                <span class="text-capitalize sheetField">{{character.ac}}</span>
                <br />
                <span class="font-weight-bolder abilityName">CHARISMA:</span>
                <span class="text-capitalize sheetSmallField">{{character.abilities.charisma}}</span>
              </b-col>

              <b-col>
                <span class="font-weight-bolder">LEVEL:</span>
                <span class="text-capitalize sheetField">{{character.level}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">XP:</span>
                <span class="text-capitalize sheetField">{{character.xp}}</span>
              </b-col>
            </b-row>
          </b-container>
        </b-card>
      </b-collapse>
    </div>
    <h1>Basic Fantasy RPG Character Creator</h1>

    <div class="border border-secondary rounded onepercent" v-if="currentsection == sections.RACE">
      <h3>Choose Your Race</h3>
      <b-form-group>
        <b-form-radio-group
          id="radioGroupRaces"
          name="radioRaces"
          buttons
          :options="raceOptions"
          size="lg"
          button-variant="outline-primary"
          v-model="character.race"
          v-on:input="setRace()"
        ></b-form-radio-group>
      </b-form-group>

      <table class="table table-striped" v-if="character.race !=''">
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
      {{errorTest}}
      <span></span>
    </div>

    <div v-if="currentsection==sections.CLASS" class="border border-secondary rounded onepercent">
      <h3>The classes</h3>
      <b-container fluid>
        <b-row class="my-1">
          <b-col>
            <b-button
              v-on:click="setClass(classes.FIGHTER)"
              size="lg"
              v-bind:variant="classQualify(classes.FIGHTER) ? 'success' : ''"
            >FIGHTER</b-button>
            <b-button
              v-on:click="setClass(classes.CLERIC)"
              size="lg"
              v-bind:variant="classQualify(classes.CLERIC) ? 'success' : ''"
            >CLERIC</b-button>
            <b-button
              size="lg"
              v-bind:variant="classQualify(classes.MAGICUSER) ? 'success' : ''"
              v-on:click="setClass(classes.MAGICUSER)"
            >MAGIC-USER</b-button>
            <b-button
              v-on:click="setClass(classes.THIEF)"
              size="lg"
              v-bind:variant="classQualify(classes.THIEF) ? 'success' : ''"
            >THIEF</b-button>
            <b-button
              size="lg"
              v-bind:variant="classQualify(classes.MAGICUSER_FIGHTER) ? 'success' : ''"
              v-on:click="setClass(classes.halfling)"
            >MAGE-FIGHTER</b-button>
            <b-button
              size="lg"
              v-bind:variant="classQualify(classes.MAGICUSER_THIEF) ? 'success' : ''"
              v-on:click="setClass(classes.halfling)"
            >MAGE-THIEF</b-button>
          </b-col>
        </b-row>
        <b-row class="my-1">
          <b-col>
            <h5>Some classes may be unavailable due to race or ability scores</h5>
          </b-col>
        </b-row>
        <b-row>
          <b-col>
            <table class="table table-striped" v-if="character.race !=''">
              <tbody>
                <tr>
                  <td colspan="2">{{classDescription}}</td>
                </tr>
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
          </b-col>
        </b-row>
      </b-container>
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
        name: "Your Characters Name",
        level: 1,
        attackbonus: 1,
        hitDice: 1,
        xp: 0,
        player: "",
        sex: "Male",
        age: 25,
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
      raceOptions: [
        { text: "Human", value: "human" },
        { text: "Elf", value: "elf" },
        { text: "Dwarf", value: "dwarf" },
        { text: "Halfling", value: "halfling" }
      ],
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
        THIEF: "Thief",
        MAGICUSER_FIGHTER: "Magic-User/Fighter",
        MAGICUSER_THIEF: "Magic-User/Thief"
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
      },
      errorTest: ""
    };
  },
  methods: {
    setRace: function() {
      switch (this.character.race) {
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
          case this.sections.ABILITIES:
            for (var key in this.character.abilities) {
              if (this.character.abilities[key] == "") {
                this.errorTest = "All abilities must be set before continuing";
                return;
              }
            }
            for (var key in this.abilityerrors) {
              if (this.abilityerrors[key] != "") {
                this.errorTest = "Please fix ability errors";
                return;
              }
            }
            this.currentsection = this.sections.CLASS;
            break;
        }
      } else {
        switch (this.currentsection) {
          case this.sections.ABILITIES:
            this.currentsection = this.sections.RACE;
            break;
          case this.sections.CLASS:
            this.currentsection = this.sections.ABILITIES;
            break;
        }
      }
    },
    disableNext() {
      if (this.currentsection.ABILITIES) {
        return true;
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
    },
    classQualify: function(classes) {
      switch (classes) {
        case this.classes.FIGHTER:
          if (this.character.abilities.strength < 9) {
            return false;
          }
          return true;
          break;
        case this.classes.CLERIC:
          if (this.character.abilities.wisdom < 9) {
            return false;
          }
          return true;
          break;
        case this.classes.MAGICUSER:
          if (
            this.character.abilities.intelligence < 9 ||
            this.character.race == this.races.DWARF ||
            this.character.race == this.races.HALFLING
          ) {
            return false;
          }
          return true;
          break;
        case this.classes.THIEF:
          if (this.character.abilities.dexterity < 9) {
            return false;
          }
          return true;
          break;
        case this.classes.MAGICUSER_FIGHTER:
          if (
            this.character.race != this.races.ELF ||
            (this.character.abilities.strength < 9 ||
              this.character.abilities.intelligence < 9)
          ) {
            return false;
          }
          return true;
          break;
        case this.classes.MAGICUSER_THIEF:
          if (
            this.character.race != this.races.ELF ||
            (this.character.abilities.dexterity < 9 ||
              this.character.abilities.intelligence < 9)
          ) {
            return false;
          }
          return true;
          break;
      }
      return true;
    },
    abilityBonus(score) {
      if (score == 3) {
        return "(-3)";
      } else if (score == 4 || score == 5) {
        return "(-2)";
      } else if (score >= 6 && score <= 8) {
        return "(-1)";
      } else if (score >= 13 && score <= 15) {
        return "(+1)";
      } else if (score == 16 || score == 17) {
        return "(+2)";
      } else if (score == 18) {
        return "(+3)";
      }
    }
  }
};
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

.sheetField {
  display: inline-block;
  border-style: solid;
  border-width: 0px 0px 2px 0px;
  width: 70%;
}

.sheetSmallField {
  display: inline-block;
  border-style: solid;
  border-width: 0px 0px 2px 0px;
  width: 20%;
}

.abilityName {
  display: inline-block;
  width: 20%;
  padding-top: 2%;
}

.editable {
  background-color: #f2f2f2;
}

.charSheet {
  background-color: #fffff8;
}
</style>
