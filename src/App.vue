<template>
  <div id="leftButton" @click="toggleEvents">
    <img src="/images/arrow-left.png" id="leftArrow">
  </div>

  <div class="arcada">
    <img src="/images/arcada.png" alt="arcada" class="arcadaLogo">
  </div>
  <div id="logoapp" class="unionLogo">
    <TheLogo />
  </div>
  <div id="rightButton" @click="toggleEvents">
    <img src="/images/arrow-right.png" id="rightArrow">
  </div>

  <div class="dateAndTime">
    <TheClock />
  </div>

  <div id="flexprkl">
    <div class="leftSide">



      <div id="menuapp" class="menu" v-show="!showEvents">
        <h1 class="todayMenu">Today's menu</h1>
        <MenuOptions />
      </div>
    </div>

    <div class="rightSide">

      <div id="classapp" class="schedule" v-show="!showEvents">
        <Classes />
      </div>

    </div>
  </div>

  <div id="eventsapp" v-show="showEvents">
    <Events />
    <Weather />
  </div>

  <div id="toDoApp" v-show="showToDo">
    <ToDo />
  </div>
</template>

<script>
import Classes from './components/Classes.vue'
import MenuOptions from './components/MenuOptions.vue'
import TheLogo from './components/TheLogo.vue'
import Events from './components/Events.vue'
import TheClock from './components/TheClock.vue'
import Weather from './components/Weather.vue'
import ToDo from './components/ToDo.vue'

export default {
  components: {
    Classes,
    MenuOptions,
    TheLogo,
    Events,
    TheClock,
    Weather,
    ToDo
  },
  data() {
    return {
      showEvents: false,
      showToDo: false
    }
  },
  methods: {
    toggleEvents() {
      this.showEvents = !this.showEvents
      //this.showToDo = !this.showToDo
    }
  }
}
</script>

<style scoped></style>
