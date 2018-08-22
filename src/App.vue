<template>
  <div id="app" style = "overflow: visible;">
    <header>
      <h1>Whiteboard</h1>
    <div>
      <button id = "add" @click="add"> Add new </button> 
      <button id = "remove" @click="remove"> Remove </button> 
    </div>
    <section v-if = "'add'">
      <textarea v-model = "message" placeholder = "ur mom gay" ></textarea>
    </section>
    </header> 
    <div class="noteboard">
      <section class = "Tasks">
        <h2> Tasks </h2>
        <draggable v-model="Tasks" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in Tasks" :key="element.id">{{element}}</div> 
        </draggable>
      </section>
      <section class = "Ongoing">
        <h2> Ongoing </h2>
        <draggable v-model="Ongoing" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in Ongoing" :key="element.id">{{element}}</div>
        </draggable>
      </section>
      <section Class = "testing">
        <h2> Testing </h2>
        <draggable v-model="testing" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in testing" :key="element.id">{{element}}</div>
        </draggable>
      </section>
      <section class = "completed">
        <h2> Completed </h2>
        <draggable v-model="completed" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in completed" :key="element.id">{{element}}</div>
        </draggable>
      </section>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "app",
  components: {
    draggable
  },

  data: {},
  methods: {
    notat: function() {
      var note = [""];
    },
    add: function() {
      if (add === true) {
        this.note = true;
      }
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  width: 980px;
  margin: 0 auto;
}
.noteboard section {
  -ms-flex: 1;
  -webkit-box-flex: 1;
  background-color: #eee;
  flex: 1;
  margin-right: 1rem;
  padding: 0.5rem;
}
.noteboard {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
}
.note {
  width: 60%;
  height: 40px;
  background-color: #eee;
  margin: auto;
  transition: width 500ms;
}
</style>