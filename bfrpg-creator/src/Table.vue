<template>
  <div id="table">
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
</template>

<script>
export default {
  name: "table",
  data() {
    return {
     
    };
  },
  computed: {
      
  },
  methods: {

  }
};
</script>

<style>

</style>
