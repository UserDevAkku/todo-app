<template>
  <div class="container">
    <div class="inputBtn">
      <q-input
        v-model="newtask"
        label="Add your task here"
        class="newinput"
      ></q-input>
      <q-btn class="button" @click="add">add task</q-btn>
      <q-list :style="style" class="list">
        <q-item
          class="item"
          v-for="(task, index) in tasks"
          :key="index"
          :style="itemStyle"
        >
          <input
            :style="
              taskeditVisible === index
                ? taskeditStyle.taskeditBGwhite
                : taskeditStyle.taskeditBGwheat
            "
            v-model="tasks[index]"
            v-if="taskeditVisible === index"
            label="Edit your task:"
          />
          <p
            :style="
              IsparaVisible === index
                ? paraStyle.paraBGwhite
                : paraStyle.paraBGwheat
            "
            v-if="IsparaVisible === index ? false : true"
          >
            {{ task }}
          </p>
          <span class="icons">
            <q-icon
              class="icon"
              color="red"
              v-if="IsVisibleRemove"
              @click="remove(index)"
              name="delete"
            ></q-icon>
            <q-icon
              class="icon"
              color="black"
              v-if="IsVisibleEdit === index ? false : true"
              @click="edit(index)"
              name="edit"
            ></q-icon>
            <q-icon
              class="icon"
              color="black"
              v-if="IsVisibleCancel"
              @click="cancel"
              name="cancel"
            ></q-icon>

            <q-icon
              class="icon"
              color="blue"
              v-if="IsVisibleSave === index ? false : true"
              @click="save(index)"
              name="save"
            ></q-icon
          ></span>
        </q-item>
      </q-list>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const newtask = ref("");
const tasks = ref([]);
const IsVisibleRemove = ref(true);
const IsVisibleEdit = ref("");
const IsVisibleCancel = ref(false);
const IsVisibleSave = ref(false);
const IsparaVisible = ref("");
const taskeditVisible = ref("");

const taskeditStyle = ref({
  taskeditBGwhite: {
    "box-shadow": "0 0 1px 1px #000",
    outline: "none",
    border: "none",
    width: "100%",
    height: "100%",
    margin: "auto",
    fontFamily:
      '"Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif',
    backgroundColor: "#ffffff",
    boxShadow: "0 0 2px 1px black",
    padding: "5px",
  },
  taskeditBGwheat: {
    "box-shadow": "0 0 2px 1px #000",
    outline: "none",
    border: "none",
    width: "100%",
    height: "100%",
    margin: "auto",
    fontFamily:
      '"Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif',
    backgroundColor: "#ffffff",
    boxShadow: "0 0 1px 1px #000",
    padding: "5px",
  },
});
const paraStyle = ref({
  paraBGwhite: {
    background: "red",
    "box-shadow": "0 0 1px 1px #000",
  },
  paraBGwheat: {
    background: "#F4E0AF",
    "box-shadow": "0 0 2px 1px white",
  },
});
const style = ref({
  "backdrop-filter": "blur(30px)",
});

const add = () => {
  if (newtask.value === "") {
    alert("pleasse add atleast one task *");
  } else {
    tasks.value.push(newtask.value);
    newtask.value = "";
  }
};
const remove = (index) => {
  tasks.value.splice(index, 1);
};
const edit = (index) => {
  IsVisibleSave.value = index;
  IsVisibleEdit.value = index;
  IsparaVisible.value = index;
  tasks.value[index] = tasks.value[index];
  taskeditVisible.value = index;
};

const save = (index) => {
  editOpt.value = true;
  saveOpt.value = false;
  parahide.value[index] = false;
  if (tasks.value[index] === newInput.value[index]) {
    alert("already exist");
  }
};

const cancel = () => {
  newInput.value = false;
  saveOpt.value = false;
  editOpt.value = true;
  cancelOpt.value = false;
  parahide.value = true;
};
</script>
<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  top: 100px;
  margin: auto;
  background-color: #d4d4d4;
  box-shadow: 0 0 5px 1px #000;
  height: max-content;
  width: 500px;
}
.newinput {
  height: 100%;
  width: 85%;
}
.button {
  background-color: yellow;
  box-shadow: 0 0 5px 1px #000;
  font-size: 10px;
  height: 100%;
  width: 15%;
  margin: auto;
  padding: 0;
  color: black;
  font-weight: bold;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.inputBtn {
  height: max-content;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  backdrop-filter: blur(40px);
  margin: 5px;
}
.list {
  width: 100%;
  height: 100%;
  margin: 5px;
}
.item {
  display: flex;
  justify-content: space-evenly;
  height: 20%;
  width: 100%;
  color: black;
  background-color: #d3f1df;
  gap: 10px;
  box-shadow: -2px 0px 1px 0px #000 inset, 2px 0px 1px 0px #000 inset;
}
.item p {
  width: 100%;
  height: 100%;
  margin: auto;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  box-shadow: 0 0 1px 1px #000;
  padding: 5px;
}
.icons {
  color: black;
  width: max-content;
  font-size: 20px;
  display: flex;
  margin: auto;
  justify-content: space-evenly;
  gap: 5px;
}
.newField {
  width: 20px;
  height: 20px;
  margin: auto;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  background-color: #f5f0cd;
  box-shadow: 0 0 1px 1px #000;
  padding: 5px;
}
</style>
