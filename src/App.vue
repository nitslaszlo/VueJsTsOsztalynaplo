<template>
  <div id="app">
    <!-- oldalcím -->
        <h1>{{ pageTitle }}</h1>
        <!-- diákok -->
        <ul>
            <li v-for="student in studentCollection" v-bind:key="student">
                <span v-bind:style="GetColor(student)">
                    {{ student.name }}
                </span>
                --
                <span v-show="student.gender == 'lány'">
                    Nőnapon virágot kap majd</span>
                <span v-if="student.gender == 'fiú'">
                    Gyereknapon labdát kap majd</span>
            </li>
        </ul>

        <!-- Új tanuló felvétele -->
        <input type="text" v-model="newStudent.name" v-on:keydown.enter="AddNewStudent()">
        <br>
        <label>
            Lány
            <input type="radio" name="gender" value="lány" v-model="newStudent.gender">
        </label>
        <label>
            Fiú
            <input type="radio" name="gender" value="fiú" v-model="newStudent.gender">
        </label>
        <br>
        <button v-on:click="AddNewStudent()">felvétel az osztályba</button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

class Student {
  name: string = "";
  gender: string = "";
}

@Component
export default class App extends Vue {
  private pageTitle: string = "Osztálynapló";
  private studentStyle = {
    color: "white",
    backgroundColor: "gray"
  };
  private newStudent = new Student();
  private studentCollection: Student[] = [
    {
      name: "Kata",
      gender: "lány"
    },
    {
      name: "Anna",
      gender: "lány"
    },
    {
      name: "Panka",
      gender: "lány"
    },
    {
      name: "Máté",
      gender: "fiú"
    },
    {
      name: "Tomi",
      gender: "fiú"
    },
    {
      name: "Andris",
      gender: "fiú"
    },
    {
      name: "Csaba",
      gender: "fiú"
    },
    {
      name: "Bence",
      gender: "fiú"
    }
  ];

  private AddNewStudent(): void {
    if (!this.newStudent.gender || !this.newStudent.name) {
      return;
    }
    this.studentCollection.push(this.newStudent);
    this.newStudent = new Student();
  }

  private GetColor(student: Student): any {
    let backgroundColor = student.gender == "fiú" ? "blue" : "red";
    return {
      color: "white",
      backgroundColor: backgroundColor
    };
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
