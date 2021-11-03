<template>
    <div id="app" @click="handleClick">
        <div class="office">
            <Map />
            <SideMenu :person="this.selectedPerson" :is-user-openned="isOpened" />
        </div>
    </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import people from "./assets/data/people.json";
import * as d3 from "d3"

export default {
  name: "App",
  components: {
    Map,
    SideMenu,
  },
  data: () => ({
    selectedPerson: null,
    isOpened: false,
    people: [],
}),
  created() {
    this.loadPeople();
  },
  methods: {
    loadPeople() {
      this.people = people;
    },
    handleClick() {
      this.isOpened = false
      const pressedTable = d3.select('g.employer-place.pressed')
      if (pressedTable._groups[0][0] !== null) {
        this.selectedPerson = this.people.find(it => it.tableId == pressedTable._groups[0][0].id)
        this.isOpened = true
      }
      pressedTable.classed('pressed', false)
    }
  }
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    color: #2c3e50;
    background-color: #fafafa;
    padding: 24px;
    box-sizing: border-box;
}

html,
body,
#app {
    height: 100%;
}

* {
    box-sizing: border-box;
}

h3 {
    margin-top: 0px;
}

.office {
    display: grid;
    grid-template-columns: 1fr 320px;
    border-radius: 6px;
    border: 1px solid #ccd8e4;
    height: 100%;
    background: white;
    max-width: 1500px;
    margin: 0 auto;
}
</style>
