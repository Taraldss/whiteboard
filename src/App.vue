<template>
  <div id="app" style = "overflow: visible;">
    <header>
      <h1>Whiteboard</h1>
    <div>
      <button id = "add" @click="add()"> Add new </button> 
      <button id = "remove" @click="remove()"> Remove </button> 
    </div>
    <section v-if="add">
      <textarea v-model="message" placeholder="ur mom gay" ></textarea>
    </section>
    </header> 
    <div class="noteboard">
      <section class="tasks">
        <h2> Tasks </h2>
        <draggable v-model="groups.tasks" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.tasks" :key="element.id">{{element.content}}</div> 
        </draggable>
      </section>
      <section class="ongoing">
        <h2> Ongoing </h2>
        <draggable v-model="groups.ongoing" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.ongoing" :key="element.id">{{element.content}}</div>
        </draggable>
      </section>
      <section class="testing">
        <h2> Testing </h2>
        <draggable v-model="groups.testing" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.testing" :key="element.id">{{element.content}}</div>
        </draggable>
      </section>
      <section class="completed">
        <h2> Completed </h2>
        <draggable v-model="groups.completed" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div v-for="element in groups.completed" :key="element.id">{{element.content}}</div>
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
      tasks: [],
      ongoing: [],
      testing: [],
      completed: [],
      message: ""
    };
  },
  methods: {
    add: function() {
      message = notes;
      if (message != "") {
        content: groups.tasks;
      }
      notes: {
        message: "";
        color: blue;
      }
    },
    remove: function() {}
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
.notes {
  color: blue($color: #000000);
}
.drag {
  min-height: 2rem;
}
</style>