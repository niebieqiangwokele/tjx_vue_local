<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>
  <button @click="mutateDeeply">

  </button>
  <div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>
  <button @click="awesome = !awesome">Toggle</button>

  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
  <li v-for="(item, index) in items" :key="item.message">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>

  <ul v-for="numbers in sets" :key="numbers">
    <li v-for="n in even(numbers)" :key="n">{{ n }}</li>
  </ul>
  <!-- `greet` 是上面定义过的方法名 -->
  <button @click="greet">Greet</button>
  <button @click="say('hello')">Say hello</button>
  <button @click="say('bye')">Say bye</button>

  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">{{ checked }}</label>
  <RouterView />

  <div>Checked names: {{ checkedNames }}</div>

  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>

  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>

  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>


  <div>Picked: {{ picked }}</div>

  <input type="radio" id="one" value="One" v-model="picked" />
  <label for="one">One</label>

  <input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>
  <!-- 
  <div>Selected: {{ selected }}</div>

  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select> -->

  <select v-model="selected">
    <option v-for="option in options" :value="option.value" :key="option.text">
      {{ option.text }}
    </option>
  </select>

  <div>Selected: {{ selected }}</div>
</template>
<script setup lang="js">
  import {
    RouterLink,
    RouterView
  } from 'vue-router'
  import HelloWorld from './components/HelloWorld.vue'
  import {
    ref
  } from 'vue'

  const obj = ref({
    nested: {
      count: 0
    },
    arr: ['foo', 'bar']
  })

  function mutateDeeply() {
    // 以下都会按照期望工作
    obj.value.nested.count++
    obj.value.arr.push('baz')
    console.log(obj.value);
  }
  const isActive = ref(true)
  const hasError = ref(false)
  let awesome = ref(true);
  const parentMessage = ref('Parent')
  const items = ref([{
    message: 'Foo'
  }, {
    message: 'Bar'
  }])

  const sets = ref([
    [1, 2, 3, 4, 5],
    [6, 7, 8, 9, 10]
  ])

  function even(numbers) {
    return numbers.filter((number) => number % 2 === 0)
  }

  const name = ref('Vue.js')

  function greet(event) {
    alert(`Hello ${name.value}!`)
    // `event` 是 DOM 原生事件
    if (event) {
      alert(event.target.tagName)
    }
  }

  function say(message) {
    alert(message)
  }
  let checked = ref();

  const checkedNames = ref([])
  const picked = ref('One')
  const selected = ref('A')

  const options = ref([{
      text: 'One',
      value: 'A'
    },
    {
      text: 'Two',
      value: 'B'
    },
    {
      text: 'Three',
      value: 'C'
    }
  ])
</script>

<style scoped>
  header {
    line-height: 1.5;
    max-height: 100vh;
  }

  .logo {
    display: block;
    margin: 0 auto 2rem;
  }

  nav {
    width: 100%;
    font-size: 12px;
    text-align: center;
    margin-top: 2rem;
  }

  nav a.router-link-exact-active {
    color: var(--color-text);
  }

  nav a.router-link-exact-active:hover {
    background-color: transparent;
  }

  nav a {
    display: inline-block;
    padding: 0 1rem;
    border-left: 1px solid var(--color-border);
  }

  nav a:first-of-type {
    border: 0;
  }

  @media (min-width: 1024px) {
    header {
      display: flex;
      place-items: center;
      padding-right: calc(var(--section-gap) / 2);
    }

    .logo {
      margin: 0 2rem 0 0;
    }

    header .wrapper {
      display: flex;
      place-items: flex-start;
      flex-wrap: wrap;
    }

    nav {
      text-align: left;
      margin-left: -1rem;
      font-size: 1rem;

      padding: 1rem 0;
      margin-top: 1rem;
    }
  }
</style>