<template>
  <div class="main">
    <div class="container">
      <ul>
        <li v-for="tab in tabs" :key="tab" @click="displayPage(tab)">{{ tab }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tabs: ["All Due", "Pending", "Auto Approval", "COMPLETED"]
    };
  },
  methods:{
    displayPage(page){
      
      console.log("This is " , page , "page");
    }
  }
};
</script>

<style>
.main {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  width: 320px;
  height: 480px;
  border: 2px solid black;
}

ul {
  padding: 0px;
  list-style-type: none;
}
li {
  padding-top: 10px;
  padding-bottom: 10px;
  font-size: 10px;
  display: inline-block;
  text-align: center;
  width: 75px;
  cursor: pointer;
  color: grey;
}
li:hover {
  color: black;
  background-color: lightgrey;
}
</style>
