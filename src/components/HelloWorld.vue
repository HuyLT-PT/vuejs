<template>
  <div class="hello" :id="msg">
    <h1>{{ msg }}</h1>
    <h1>{{ from }}</h1>
    <button :disabled=true>button is disabled</button>
    <button v-bind="attribute">button is disabled</button>
    <button v-bind="attribute" @click="change">{{ age }}</button>
    <button v-bind="attribute" @click="change">{{userInfo.age}}</button>
    <button v-bind="attribute" @click="changeFullName">{{fullName}}</button>
    <button class="button active">Click me</button>
    <!-- binding by object -->
    <button class="button" :class="activeObject" @click="changeActive">Click me</button> 
    <!-- binding by class -->
    <button class="button" :class="['active']">Done click me</button>
    <!-- inline-->
    <button style="color: yellow; background-color: blueviolet;">Inline</button>
    <button :style="{
      color:'yellow',
      background:'blueviolet'
    }">Inline Binding</button>
    <br/>
    <!--v-if-->
    <h1 v-if="condition" @click="login">Login</h1>
    <h1 v-else @click="login">Logout</h1>
    <!--v for-->
    <ul>
      <li v-for="item in array" :key="item.name"> {{ item.name }} - {{ item.age }}</li>      
    </ul>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
import { computed, reactive, ref } from 'vue';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup(){
    const from = "From Hanoi"
    const attribute = {
      disabled : false,
      style : {
        color :"red"
      }
    }
    const age = ref(10)
    const userInfo = reactive({
      age:10,
      name : "huy",
      items:[1,2,3,4,5]
    })

    const change = () => {
      age.value++;
      userInfo.age++;
    }
    const firstName = ref("1")
    const lastName = ref("2")
    const fullName = computed({
      get: () => `${firstName.value} ${lastName.value}`,
      set: (newValue) => {
      [firstName.value, lastName.value = ""] = newValue.split(" ");
      },
    });

    const changeFullName = () => {
      change()
      fullName.value = `1 ${age.value}`;
    }

    //binding
    const isActive = ref(true)
    const changeActive = () => {
      isActive.value = !isActive.value
    }

    const activeObject = computed(()=>{
      return {
        active : isActive.value
      }
    })

    //v-if
    const condition = ref(true)
    const login = () =>{
      condition.value = !condition.value
    }

    //v-for
    const array = ref([{
      name: 'Huy',
      age: 18
    },{
      name: 'Huy Ne',
      age: 19
    }])
    return {
      from, 
      attribute,
      age,
      userInfo,
      fullName,
      isActive,
      activeObject,
      condition,
      array,
      change,
      changeFullName,
      changeActive,
      login
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.button {
  border-radius: 15%;
}
.active {
  color: #42b983;
  background: #42b983;
  cursor: pointer;
  
  /* &:hover {
    background: white;
  } */
}

.active:hover {
  background: white;
}

</style>
