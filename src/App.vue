<template>
  <div id="app" style = "overflow: visible;" >
    <header>
    <div>
      <h1 class = "heading">Whiteboard</h1>
      <button @click="add()" class="button"> + </button> 
      <button @click="remove()" class="button"> - </button> 
    </div>
    <section v-if="add">
      <textarea v-model="message" placeholder="new task" class="messageBoard" ></textarea>
    </section>
    <section v-if="remove">

    </section>
    </header> 
    <div class="noteboard">
      <section class="tasks">
        <h2> Tasks </h2>
        <draggable v-model="groups.tasks" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.tasks" :key="element.id">{{element}}</div> 
        </draggable>
      </section>
      <section class="ongoing">
        <h2> Ongoing </h2>
        <draggable v-model="groups.ongoing" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.ongoing" :key="element.id">{{element}}</div>
        </draggable>
      </section>
      <section class="testing">
        <h2> Testing </h2>
        <draggable v-model="groups.testing" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.testing" :key="element.id">{{element}}</div>
        </draggable>
      </section>
      <section class="completed">
        <h2> Completed </h2>
        <draggable v-model="groups.completed" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.completed" :key="element.id">{{element}}</div>
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

  data: function() {
    return {
      groups: {
        tasks: [],
        ongoing: [],
        testing: [],
        completed: []
      },
      message: ""
      
    };
  },
  methods: {
    add: function() {
      if (this.message != "") {
        this.groups.tasks.push(this.message);
      }
    },
    remove: function() {
      this.groups.tasks.splice(this.message, 1);
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
  //padding: 180px;
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
.heading {
  color: black;
}
.noteboard {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
}
.notes {
  color: blue($color: #000000);
}
.drag {
  min-height: 2rem;
  color: black;
  padding: 0, 5rem;
  background-color: yellow;
}
</style>