<template>
  <div class="hello">
    <div class="container">
      <h2 class="title">{{ title }}</h2>
      <form class="first_form" action="#">
        <input
          v-bind:placeholder="myPlaceholder"
          v-model="inputValue"
          v-on:keypress.enter="addNewNote"
          type="text"
        />
        <button type="submit" v-on:click.prevent="addNewNote">Add</button>
      </form>
      <h3 class="title">{{ subTitle }}</h3>
      <ul class="list">
        <li class="list_item" v-for="(myNote, index) in notes" :key="myNote.value">
          <div class="item" v-if="!myNote.isComplete">
            <input
              type="checkbox"
              v-model="myNote.isComplete"
              v-on:click="doComplete(index)"
            />
            <input v-if="myNote.isEditing" type="text" v-model="myNote.value"/>
            <p v-else>{{ myNote.value }}</p>

            <button type="submit" v-on:click="editTask(index)">
              Edit
            </button>
            <button type="reset" v-on:click="removeNote(index)">Delette</button>
          </div>
        </li>
      </ul>
      <h3 class="title">Completed</h3>
      <ul>
        <li class="list_item" v-for="(myNote, index) in notes" :key="myNote.value">
          <div class="item" v-if="myNote.isComplete">
            <input
              type="checkbox"
              v-model="myNote.isComplete"
              v-on:click="undoComplete(index)"
            />
            <input v-if="myNote.isEditing" type="text" v-model="myNote.value"/>
            <p v-else>{{ myNote.value }}</p>
            <button type="submit" v-on:click="editTask(index)">
              Edit
            </button>
            <button type="reset" v-on:click="removeNote(index)">Delette</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      title: "Add item",
      subTitle: "todo",
      myPlaceholder: "Enter your task for today",
      inputValue: '',
      isValue: false,
      notes:[ 
        { id: 1, value: "значення 1", isComplete: false},
        { id: 2, value: "значення 2", isComplete: false}
        ],
    }
  },
  methods: {
    editTask(index) {
      let mode = !this.notes[index].isEditing;
      this.notes[index].isEditing = mode;
    },
    addNewNote() {
      if (this.inputValue !== "") {
        this.notes.push({value: this.inputValue, isComplete: false});
        this.inputValue = "";
        console.log('addNewNote', this.notes)
      }
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
    doComplete(index) {
      this.notes[index].isComplete = true;
    },
    undoComplete(index) {
      this.notes[index].isComplete = false;
    },
  },
};
</script>

<style scoped>
h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0;
  padding: 0;
}
p {
  margin: 0 10px;
  width: 100%;
}
ul {
  padding: 0;
  margin: 0;
}
li {
  list-style: none;
  text-decoration: none;
}
.hello {
  max-width: 1200px;
  width: 100;
  margin: 0 auto;
  padding: 20px;
}
.container {
  max-width: 800px;
  width: 100%;
  padding: 50px 0;
  margin: 0 auto;
}
.title {
  text-transform: uppercase;
  color: #000;
  padding-bottom: 10px;
  border-bottom: 4px solid #000;
  margin-bottom: 20px;
}
.list_item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}
.item {
  display: flex;
  width: 100%;
  align-items: center;
  margin-block: 10px;
}

/* form */
.first_form {
  display: flex;
  margin-bottom: 30px;
  gap: 10px;
}
label {
  padding: 5px 10px;
  width: 100%;
}
input[type="text"] {
  flex-grow: 1;
  margin: 0 10px;
  width: 100%;
  border: 1px solid #aaa;
  padding: 5px 10px;
  background: #fff;
  border-radius: 6px;
  transition: color 0.3s ease-in, border-color 0.3s ease-in,
    background-color 0.3s ease-in, opacity 0.3s ease-in;
}
input[type="text"]:focus {
  outline: none;
  box-shadow: 0 0 5px #ce33e2;
}
</style>
