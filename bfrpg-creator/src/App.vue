<template>
  <div id="app">
    <div>
      <b-button v-b-toggle.collapse-1 variant="primary" class="fixed-top right">Character Sheet</b-button>
      <b-collapse id="collapse-1" class="mt-2">
        <b-card
          class="border border-secondary rounded floatingheader onepercent text-left charSheet"
          id="characterSheet"
        >
          <b-container fluid>
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
                <span class="text-capitalize sheetSmallField editable" contenteditable="true"></span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">XP:</span>
                <span class="text-capitalize sheetSmallField editable" contenteditable="true"></span>
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
                <span class="text-capitalize sheetSmallField editable" contenteditable="true"></span>
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
                <span class="font-weight-bolder abilityName">AC:</span>
                <span class="text-capitalize sheetSmallField"></span>
                <br />
                <span class="font-weight-bolder abilityName">AB:</span>
                <span class="text-capitalize sheetSmallField editable" contenteditable="true"></span>
                <br />
                <span class="font-weight-bolder abilityName">HP:</span>
                <span class="text-capitalize sheetSmallField editable" contenteditable="true"></span>
                <br />
                <span class="font-weight-bolder abilityName">HD:</span>
                <span class="text-capitalize sheetSmallField">{{character.hitDice}}</span>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">MOVE:</span>
                <span class="text-capitalize sheetSmallField editable" contenteditable="true"></span>
                <br />
                <br />
                <span class="font-weight-bolder">MONEY:</span>
                <span>
                  <br />
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                </span>
              </b-col>
            </b-row>
            <b-row class="my-1 pb-4">
              <b-col>
                <span class="font-weight-bolder">SPELLS/ABILITIES:</span>
                <p class="mb-5">
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                </p>
                <span class="font-weight-bolder mt-5">EQUIPMENT:</span>
                <p>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetField editable pb-2" contenteditable="true"></span>
                </p>
              </b-col>
              <b-col>
                <span class="font-weight-bolder">SAVING THROWS:</span>
                <p class="ml-4">
                  <span class="font-weight-bold abilityName">Death Ray/Poison:</span>
                  <span class="text-capitalize sheetSmallField">{{character.saves.deathray}}</span>
                  <br />
                  <span class="font-weight-bolder abilityName">Magic Wands:</span>
                  <span class="text-capitalize sheetSmallField pb-4">{{character.saves.magicWands}}</span>
                  <br />
                  <span class="font-weight-bolder abilityName">Paralysis/Turn to Stone:</span>
                  <span class="text-capitalize sheetSmallField pb-4">{{character.saves.paralysis}}</span>
                  <br />
                  <span class="font-weight-bolder abilityName">Dragon Breath:</span>
                  <span
                    class="text-capitalize sheetSmallField pb-4"
                  >{{character.saves.dragonBreath}}</span>
                  <br />
                  <span class="font-weight-bolder abilityName">Spells:</span>
                  <span class="text-capitalize sheetSmallField pb-4">{{character.saves.spells}}</span>
                </p>
                <p class="mt-5">
                  <span class="font-weight-bold">WEAPON:</span>

                  <span class="font-weight-bold ml-5">AB:</span>

                  <span class="font-weight-bold ml-5">DAMAGE:</span>

                  <span class="font-weight-bold ml-5">RANGE:</span>
                  <br />
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                </p>
                <p></p>
              </b-col>
            </b-row>
            <b-row>
              <b-col>
                <span class="font-weight-bolder">NOTES (kills, events, relationships):</span>
                <p>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                  <span class="text-capitalize sheetFieldFull editable pb-2" contenteditable="true"></span>
                </p>
              </b-col>
            </b-row>
            <b-row>
              <b-col>
                <b-button
                  variant="primary"
                  size="lg"
                  class="printerButton"
                  v-on:click="printCharacterSheet()"
                >PRINT SHEET</b-button>
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
                <b-col class="border dieRoll">
                  <span>{{randomroll.one}}</span>
                </b-col>
                <b-col class="border dieRoll">
                  <span>{{randomroll.two}}</span>
                </b-col>
                <b-col class="border dieRoll">
                  <span>{{randomroll.three}}</span>
                </b-col>
                <b-col class="border dieTotal">
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
                    placeholder="+ to attack and damage rolls with melee or thrown weapons"
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
                    placeholder="+ to range attack rolls, armor class, initiative rolls"
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
                    placeholder="+ languages known, save vs. illusion"
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
                    placeholder="+ some saving throws vs. magical attacks"
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
                    placeholder="+ to hit points and save vs. poison"
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
                    placeholder="+ morale reaction rolls, number of retainers"
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
              v-on:click="showClass(classes.FIGHTER)"
              size="lg"
              v-bind:variant="classQualify(classes.FIGHTER) ? 'success' : ''"
            >FIGHTER</b-button>
            <b-button
              v-on:click="showClass(classes.CLERIC)"
              size="lg"
              v-bind:variant="classQualify(classes.CLERIC) ? 'success' : ''"
            >CLERIC</b-button>
            <b-button
              size="lg"
              v-bind:variant="classQualify(classes.MAGICUSER) ? 'success' : ''"
              v-on:click="showClass(classes.MAGICUSER)"
            >MAGIC-USER</b-button>
            <b-button
              v-on:click="showClass(classes.THIEF)"
              size="lg"
              v-bind:variant="classQualify(classes.THIEF) ? 'success' : ''"
            >THIEF</b-button>
            <b-button
              size="lg"
              v-bind:variant="classQualify(classes.MAGICUSER_FIGHTER) ? 'success' : ''"
              v-on:click="showClass(classes.MAGICUSER_FIGHTER)"
            >MAGE-FIGHTER</b-button>
            <b-button
              size="lg"
              v-bind:variant="classQualify(classes.MAGICUSER_THIEF) ? 'success' : ''"
              v-on:click="showClass(classes.MAGICUSER_THIEF)"
            >MAGE-THIEF</b-button>
          </b-col>
        </b-row>
        <b-row class="my-1">
          <b-col>
            <h5>Available classes in green. Others are unavailable due to race or ability scores</h5>
          </b-col>
        </b-row>
        <b-row>
          <b-col>
            <table class="table table-striped" hover v-if="clickedClass != ''">
              <tbody>
                <tr>
                  <td colspan="2" class="font-italic font-weight-bold">
                    <h3>{{clickedClass}}</h3>
                    {{classDescription}}
                  </td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right" style="width: 50%">Prime Requisite</td>
                  <td class="text-left" role="cell">{{classTable.primeRequisite}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">Hit Dice</td>
                  <td class="text-left">{{classTable.hitDice}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">Weapons</td>
                  <td class="text-left">{{classTable.weapons}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">Armor</td>
                  <td class="text-left">{{classTable.armor}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">2nd level XP</td>
                  <td class="text-left">{{classTable.xpForSecond}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">Spells</td>
                  <td class="text-left">{{classTable.spells}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">Special</td>
                  <td class="text-left">{{classTable.special}}</td>
                </tr>
                <tr>
                  <td class="font-weight-bold text-right">1st level saves</td>
                  <td class="text-left" v-html="classTable.firstLevelSaves"></td>
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
            v-on:click="changeSection('next')"
            :disabled="nextDisabled"
            v-if="currentsection != sections.FINAL"
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
        hitDice: "",
        player: "",
        sex: "Male",
        abilities: {
          strength: "",
          dexterity: "",
          intelligence: "",
          wisdom: "",
          constitution: "",
          charisma: ""
        },
        saves: {
          deathray: "",
          magicWands: "",
          paralysis: "",
          dragonBreath: "",
          spells: ""
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
        CLASS: "class",
        FINAL: "final"
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
      errorTest: "",
      clickedClass: "",
      classDescription: "",
      classTable: {
        primeRequisite: "",
        hitDice: "",
        weapons: "",
        armor: "",
        xpForSecond: "",
        spells: "",
        special: "",
        firstLevelSave: ""
      },
      nextDisabled: false
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
            this.nextDisabled = false;
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
            this.nextDisabled = true;
            break;
          case this.sections.CLASS:
            this.setClassAndSavingThrows();
            this.currentsection = this.sections.FINAL;
            return;
        }
      } else {
        switch (this.currentsection) {
          case this.sections.ABILITIES:
            this.currentsection = this.sections.RACE;
            this.nextDisabled = false;
            break;
          case this.sections.CLASS:
            this.currentsection = this.sections.ABILITIES;
            this.nextDisabled = false;
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
    },
    showClass: function(classClicked) {
      this.clickedClass = classClicked;
      this.nextDisabled = false;
      if (!this.classQualify(classClicked)) {
        this.nextDisabled = true;
      }

      switch (classClicked) {
        case this.classes.FIGHTER:
          this.classDescription =
            "Fighters include soldiers, guardsmen, barbarian warriors, and anyone else for whom fighting is a way of life. They train in combat, and they generally approach problems head on, weapon drawn.";
          this.classTable.primeRequisite = "STR (must be 9+)";
          this.classTable.hitDice = "d8";
          this.classTable.weapons = "Any";
          this.classTable.armor = "Any, shields allowed";
          this.classTable.xpForSecond = "2000";
          this.classTable.spells = "None";
          this.classTable.special = "None";
          this.classTable.firstLevelSaves =
            "<ol><li>Death Ray or Poison: 12</li><li>Magic Wands: 13</li><li>Paralysis or Petrify: 14</li><li>Dragon Breath: 15</li><li>Spells: 17</li></ol>";
          break;

        case this.classes.CLERIC:
          this.classDescription =
            "Clerics are those who have devoted themselves to the service of a deity, pantheon or other belief system. They are called to go abroad from the temple and serve their deity in a more direct way, smiting undead monsters and aiding in the battle against evil and chaos.";
          this.classTable.primeRequisite = "WIS (must be 9+)";
          this.classTable.hitDice = "d6";
          this.classTable.weapons =
            "Blunt weapons only (clubs, maces, mauls, quarterstaves, slings, warhammers)";
          this.classTable.armor = "Any, shields allowed";
          this.classTable.xpForSecond = "1500";
          this.classTable.spells = "None at first level";
          this.classTable.special = "Turn undead";
          this.classTable.firstLevelSaves =
            "<ol><li>Death Ray or Poison: 11</li><li>Magic Wands: 12</li><li>Paralysis or Petrify: 14</li><li>Dragon Breath: 16</li><li>Spells: 15</li></ol>";
          break;

        case this.classes.MAGICUSER:
          this.classDescription =
            "Magic-Users are those who seek and use knowledge of the arcane. They do magic not as the Cleric does, by faith in a greater power, but rather through insight and understanding";
          this.classTable.primeRequisite = "INT (must be 9+)";
          this.classTable.hitDice = "d4";
          this.classTable.weapons = "Cudgel, dagger, walking staff";
          this.classTable.armor = "None";
          this.classTable.xpForSecond = "2500";
          this.classTable.spells = "1 first level spell";
          this.classTable.special = "None";
          this.classTable.firstLevelSaves =
            "<ol><li>Death Ray or Poison: 13</li><li>Magic Wands: 14</li><li>Paralysis or Petrify: 13</li><li>Dragon Breath: 16</li><li>Spells: 15</li></ol>";
          break;

        case this.classes.THIEF:
          this.classDescription =
            "Thieves are those who take what they want or need by stealth, disarming traps and picking locks to get to the gold they crave; or “borrowing” money from pockets, beltpouches, etc. right under the nose of the 'mark' without the victim ever knowing.";
          this.classTable.primeRequisite = "DEX (must be 9+)";
          this.classTable.hitDice = "d4";
          this.classTable.weapons = "Any";
          this.classTable.armor = "Leather, no shield";
          this.classTable.xpForSecond = "1250";
          this.classTable.spells = "None";
          this.classTable.special = "Sneak attack plus Thieves abilities";
          this.classTable.firstLevelSaves =
            "<ol><li>Death Ray or Poison: 13</li><li>Magic Wands: 14</li><li>Paralysis or Petrify: 13</li><li>Dragon Breath: 16</li><li>Spells: 15</li></ol>";
          break;

        case this.classes.MAGICUSER_FIGHTER:
          this.classDescription =
            "Must meet the requirements of both classes. Combination class characters use the best attack bonus and the best saving throw values of their original two classes, BUT MUST GAIN XP EQUAL TO THE COMBINED REQUIREMENTS OF BOTH CLASSES TO ADVANCE IN LEVELS. May both fight and cast magic spells; further, they are allowed to cast magic spells while wearing armor. These characters roll six-sided dice (d6) for hit points.";
          this.classTable.primeRequisite = "INT, STR (must be 9+)";
          this.classTable.hitDice = "d6";
          this.classTable.weapons = "Any";
          this.classTable.armor = "Any, shields allowed";
          this.classTable.xpForSecond = "2000 + 2500";
          this.classTable.spells = "1 first level spell";
          this.classTable.special = "None";
          this.classTable.firstLevelSaves =
            "<ol><li>Death Ray or Poison: 13</li><li>Magic Wands: 14</li><li>Paralysis or Petrify: 14</li><li>Dragon Breath: 16</li><li>Spells: 17</li></ol>";
          break;

        case this.classes.MAGICUSER_THIEF:
          this.classDescription =
            "Must meet the requirements of both classes. Combination class characters use the best attack bonus and the best saving throw values of their original two classes, BUT MUST GAIN XP EQUAL TO THE COMBINED REQUIREMENTS OF BOTH CLASSES TO ADVANCE IN LEVELS. Members of this combination class may cast spells while wearing leather armor, and may useany weapon. ";
          this.classTable.primeRequisite = "INT, DEX (must be 9+)";
          this.classTable.hitDice = "d4";
          this.classTable.weapons = "Any";
          this.classTable.armor = "Leather, no shield";
          this.classTable.xpForSecond = "1250 + 2500";
          this.classTable.spells = "1 first level spell";
          this.classTable.special = "Sneak attack plus Thieves abilities";
          this.classTable.firstLevelSaves =
            "<ol><li>Death Ray or Poison: 13</li><li>Magic Wands: 14</li><li>Paralysis or Petrify: 13</li><li>Dragon Breath: 16</li><li>Spells: 15</li></ol>";
          break;
      }
    },
    setClassAndSavingThrows: function() {
      var deathRayBonus = 0;
      var magicWandsBonus = 0;
      var paralysisBonus = 0;
      var dragonBreathBonus = 0;
      var spellsBonus = 0;

      this.character.class = this.clickedClass;

      switch (this.character.race) {
        case this.races.DWARF:
        case this.races.HALFLING:
          deathRayBonus = 4;
          magicWandsBonus = 4;
          paralysisBonus = 4;
          dragonBreathBonus = 3;
          spellsBonus = 4;
          break;
        case this.races.ELF:
          magicWandsBonus = 2;
          paralysisBonus = 1;
          spellsBonus = 2;
          break;
      }

      switch (this.character.class) {
        case this.classes.FIGHTER:
          if (
            this.character.race == this.races.ELF ||
            this.character.race == this.races.HALFLING
          ) {
            this.character.hitDice = "d6";
          } else {
            this.character.hitDice = "d8";
          }
          this.character.saves.deathray = 12 + deathRayBonus;
          this.character.saves.magicWands = 13 + magicWandsBonus;
          this.character.saves.paralysis = 14 + paralysisBonus;
          this.character.saves.dragonBreath = 15 + dragonBreathBonus;
          this.character.saves.spells = 17 + spellsBonus;
          break;
        case this.classes.CLERIC:
          this.character.hitDice = "d6";
          this.character.saves.deathray = 11 + deathRayBonus;
          this.character.saves.magicWands = 12 + magicWandsBonus;
          this.character.saves.paralysis = 14 + paralysisBonus;
          this.character.saves.dragonBreath = 16 + dragonBreathBonus;
          this.character.saves.spells = 15 + spellsBonus;
          break;
        case this.classes.MAGICUSER:
          this.character.hitDice = "d4";
          this.character.saves.deathray = 11 + deathRayBonus;
          this.character.saves.magicWands = 12 + magicWandsBonus;
          this.character.saves.paralysis = 14 + paralysisBonus;
          this.character.saves.dragonBreath = 16 + dragonBreathBonus;
          this.character.saves.spells = 15 + spellsBonus;
          break;
        case this.classes.THIEF:
          this.character.hitDice = "d4";
          this.character.saves.deathray = 11 + deathRayBonus;
          this.character.saves.magicWands = 12 + magicWandsBonus;
          this.character.saves.paralysis = 14 + paralysisBonus;
          this.character.saves.dragonBreath = 16 + dragonBreathBonus;
          this.character.saves.spells = 15 + spellsBonus;
          break;
      }
    },
    printCharacterSheet() {
      var newWindow = window.open();
      newWindow.document.write(
        "<html><head><title>" + document.title + "</title>"
      );
      newWindow.document.write(
        '<link rel="stylesheet" href="/dist/main.css" type="text/css" />'
      );
      newWindow.document.write(
        '<link rel="stylesheet" href="/src/assets/print.css" type="text/css" />'
      );
      newWindow.document.write("</head><body >");
      newWindow.document.write("<h1>" + document.title + "</h1>");
      newWindow.document.write(
        document.getElementById("characterSheet").innerHTML
      );
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

.sheetFieldFull {
  display: inline-block;
  border-style: solid;
  border-width: 0px 0px 2px 0px;
  width: 98%;
}

.sheetSmallField {
  display: inline-block;
  border-style: solid;
  border-width: 0px 0px 2px 0px;
  width: 25%;
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

.dieRoll {
  background-color: ghostwhite;
}

.dieTotal {
  background-color: palegreen;
}
</style>
