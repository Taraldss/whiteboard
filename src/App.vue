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
    <div>
      <button @click="save()">Save all notes</button>
    </div>
    <div class="noteboard">
      <section class = "Tasks">
        <h2> Tasks </h2>
        <draggable v-model="Tasks" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in Tasks" :key="element.id">
          {{element}}
          <button :class="{show: showRemove}" @click="remove(index,'tasks')">x</button>
          </div> 
        </draggable>
      </section>
      <section class = "Ongoing">
        <h2> Ongoing </h2>
        <draggable v-model="Ongoing" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in Ongoing" :key="element.id">
            {{element}}
         <button :class="{show: showRemove}" @click="remove(index,'tasks')">x</button>
         </div>
        </draggable>
      </section>
      <section Class = "testing">
        <h2> Testing </h2>
        <draggable v-model="testing" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in testing" :key="element.id">
            {{element}}
          <button :class="{show: showRemove}" @click="remove(index,'tasks')">x</button>
          </div>
        </draggable>
      </section>
      <section class = "completed">
        <h2> Completed </h2>
        <draggable v-model="completed" :options="{group:'sections'}" @start="drag=true" @end="drag=false">
          <div v-for="element in completed" :key="element.id">
          {{element}}
          <button :class="{show: showRemove}" @click="remove(index,'tasks')">x</button>
          </div>
        </draggable>
      </section>
    </div>
    <div>{{groups}}</div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import axios from "axios";

export default {
  name: "app",
  components: {
    draggable
  },

  data: function() {
    return {
    groups: [
      {
    name: "tasks",
    issues: []
      },
      {
    name: "ongoing",
    issues: []
      },
      {
    name: "testing",
    issues: []
      },
      {
    name: "completed",
    issues: []
      }
    ],
    message: "",
    showRemove: false,
    apiKey: "$2a$10$7ZaK7Pyn.yLeaCSbTHR4i.Tlh.zLpGgkm1qP1y5FOCH5sOFkLFw3a",
    binUrl: "https://api.jsonbin.io/b/5bfd8966df915b653998c24c",
    };
  },
computed:{

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
    },
    load: function() {
      let self = this
      axios.get(self.binUrl, {
          headers: { "secret-key": self.apiKey, versioning: false }}).then( function(response) {
            self.groups = response.data
          }).catch(function(error) {
            console.log(error)
          })
    },
    save: function() {
      let self = this
      axios
        .put(self.binUrl, self.groups, {
          headers: { "secret-key": self.apiKey, versioning: false }
        })
        //puts the group data into jsonbin, as json code
        .then(function(response) {
          // handle success
        })
        .catch(function(error) {
          // handle error
          console.log(error);
        })
    }
  },
  beforeMount() {
    this.load()
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
.noteboard {
  button {
    display: none;
  }
  button.show {
    display: inline-block;
  }
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
}
.heading {
  color: black;
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