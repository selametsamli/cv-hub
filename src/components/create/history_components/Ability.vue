<template>
  <div id="ability" class="ability">

    <h3 class="ability-title">Yetenekler ({{abilityData.abilityList.length}})</h3>

    <div v-if="abilityData.abilityList.length>0" class="ability-summary">
      <ul class="list-group ability-summary-list">
        <li v-for="(ab,index) in abilityData.abilityList" class="list-group-item">

          <div class=" float-left">{{ab.name}} {{index}}</div>
          <div class=" float-right control-panel">
            <button @click="destroyAbility(index)" class=" btn btn-outline-dar btn-sm">X</button>
            <button @click="editAbility(index)" class=" btn btn-outline-dar btn-sm">D</button>
          </div>
        </li>
      </ul>
    </div>

    <form class="select-div" v-if="abilityData.formShow">
      <div class="select-option">
        <div class="col-md-6 mb-3 pl-0">
          <label class="sm-title">Beceri</label>
          <input v-model="abilityData.ability.name" type="text" class="form-input" placeholder="Örn. Microsoft Word"
                 required>
        </div>
        <div class="col-md-6 mb-3 pr-0">
          <label class="sm-title">Seviye</label>
          <select v-model="abilityData.ability.level" class="form-select ">
            <option disabled selected>Seç</option>
            <option :value="key" v-for="(level,key) in abilityData.abilityLevel">{{level}}</option>


          </select>
        </div>


      </div>
    </form>
    <div id="buttons">
      <div class="buttons-block">
        <button class="ability-button-remove">Sil</button>
        <button :disabled="saveEnabled" @click="addAbility(abilityData.ability)" class="ability-button-save">Kaydet</button>
      </div>
      <div class="others-block">
        <button @click="addNewAbility()" class="ability-button-other">Başka bir beceri
          ekle
        </button>
      </div>
    </div>

  </div>
</template>

<script>
  import {mapGetters, mapMutations} from "vuex"

  export default {

    methods: {
      ...mapMutations([
        'addNewAbility',
        'destroyAbility',
        'editAbility',
        'addAbility'

      ]),


    },
    computed: {
      ...mapGetters({
        abilityData: 'getAbilityData'
      }),

      // ---------------------------  u  g  i  --------------------
      saveEnabled () {
        if (this.abilityData.ability.name.length > 0 && this.abilityData.ability.level > 0){
          return false;
        }
        else {
          return true;
        }
      }
      // ----------------------------------------------------------
    }
  }

</script>

<style lang="scss" scoped>

  //---------------------------------

  a, button, input, select, option {
    outline: none;
    font-family: sans-serif;
  }

  select {
    //-webkit-appearance: none;
    //-moz-appearance: none;
    //text-indent: 5px;
    //text-overflow: '';
    position: center;

  }

  body {
    font-family: 'Muli', sans-serif;
  }
  //---------------------------------

  .sm-title {
    color: #9aa4ae;
    font-family: sans-serif;
    font-weight: 400;
    font-size: 12px;
    text-transform: uppercase;
  }

  .form-input {
    padding-left: 15px;
    width: 100%;
    height: 45px;
    border: 1.4px solid #eaeaea;
    border-radius: 4px;

    &:focus {
      border: 2px solid #eaeaea;
    }
  }

  .form-select {
    appearance: none;
    background-color: transparent;
    width: 100%;
    height: 45px;
    border: 1.4px solid #eaeaea;
    border-radius: 4px;
  }

  .select-div {
    width: 100%;
    padding-left: 0px;
    margin-left: 0px;
  }

  .select-option {
    padding: 0px;
    display: flex;
    width: 100%;
    justify-content: flex-start;

  }

  .ability {
    width: 70%;
    background-color: white;
    height: auto;
    display: flex;
    flex-wrap: wrap;
    margin-left: auto;
    margin-right: auto;
    padding: 45px 45px;
    -webkit-box-shadow: 0px 0px 17px 0px rgba(0,0,0,0.66);
    -moz-box-shadow: 0px 0px 17px 0px rgba(0,0,0,0.66);
    box-shadow: 0px 0px 25px 0px rgba(0,0,0,0.15);
    border-radius: 4px;
    margin-top: 100px;

    &-title {
      font-size: 22px;
      letter-spacing: .6px;
      color: rgb(0,0,0,0.8);
    }

    &-summary {
      width: 100%;
      height: auto;
      display: flex;
      flex-wrap: nowrap;
      flex-direction: row;
      justify-content: flex-start;
      align-items: center;
      margin-top: 10px;
      margin-bottom: 20px;

      &-list {
        width: 100%;
      }
    }

    #buttons {
      width: 100%;
      height: 50px;
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;

      .buttons-block {
        width: 50%;
        display: flex;
        justify-content: flex-start;
        align-items: center;
      }

      .others-block {
        width: 50%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
      }
    }

    &-button-remove {

      margin-right: 5px;
      font-weight: 400;
      border: none;
      font-size: 15px;
      color: #565a74;
      width: 85px;
      height: 40px;
      border-radius: 4px;
      background-color: #ecf1f5;
      transition: all .3s;

      &:hover {
        background-color: transparent;
        font-weight: 700;
        cursor: pointer;
        border: none;

      }
    }

    &-button-save {

      margin-left: 5px;
      font-weight: 400;
      border: none;
      color: white;
      width: 85px;
      height: 40px;
      font-size: 15px;
      border-radius: 4px;
      background-color: #3d64ff;
      transition: all .3s;

      &:hover {
        background-color: transparent;
        font-weight: 700;
        cursor: pointer;
        color: #565a74;
      }
    }

    &-button-other {

      border: none;
      background-color: #ecf1f5;
      width: auto;
      border-radius: 4px;
      padding-left: 22.5px;
      padding-right: 22.5px;
      height: 40px;
      font-size: 15px;
      font-weight: 400;
      color: #565a74;

      transition: all .3s;

      &:hover {
        background-color: transparent;
        cursor: pointer;
        color: #565a74;
      }
    }
  }


</style>
