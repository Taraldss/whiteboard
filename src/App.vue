<template>
  <div id="app" style = "overflow: visible;" >
    <header>
    <div>
      <h1 class = "heading">Whiteboard</h1>
      <button @click="add()" class="button"> Add Task </button> 
       <button @click="toggleRemove()">Remove Task</button>
    </div>
    <section v-if="add">
      <textarea v-model="message" placeholder="new task" class="messageBoard" ></textarea>
    </section>
    </header> 
    <div class="noteboard">
      <section class="tasks">
        <h2> Tasks </h2>
        <draggable v-model="groups.tasks" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div class="task" v-for="(element, index) in groups.tasks" :key="index">
            {{element}}
            <button :class="{show: showRemove}" @click="remove(index,'tasks')">x</button>
          </div>         
        </draggable>
      </section>
      <section class="ongoing">
        <h2> Ongoing </h2>
        <draggable v-model="groups.ongoing" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div class="ongoing" v-for="(element, index) in groups.ongoing" :key="index">
            {{element}}
            <button :class="{show: showRemove}" @click="remove(index,'ongoing')">x</button>
          </div> 
        </draggable>
      </section>
      <section class="testing">
        <h2> Testing </h2>
        <draggable v-model="groups.testing" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div class="testing" v-for="(element, index) in groups.testing" :key="index">
            {{element}}
            <button :class="{show: showRemove}" @click="remove(index,'testing')">x</button>
          </div>         
        </draggable>
      </section>
      <section class="completed">
        <h2> Completed </h2>
        <draggable v-model="groups.completed" :options="{group:'sections'}" @start="drag=true" @end="drag=false" class="drag">
          <div class="completed" v-for="(element, index) in groups.completed" :key="index">
            {{element}}
            <button :class="{show: showRemove}" @click="remove(index,'completed')">x</button>
          </div>         
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
      message: "",
      showRemove: false,
    };
  },
  methods: {
    add: function() {
      if (this.message != "") {
        this.groups.tasks.push(this.message);
      }
    },
    toggleRemove: function() {
      this.showRemove = !this.showRemove;
    },
    remove: function(index, group) {
      this.groups[group].splice(index, 1);
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
.task {
  button {
    display: none;
  }
  button.show {
    display: inline-block;
  }
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
}
</style>