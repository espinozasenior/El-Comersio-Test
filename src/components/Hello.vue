<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Bellow put some number to sort:</h2>
    <form role="form" class="form">
      <input type="number" name="inputNumber" id="inputNumber" v-model="number"/>
      <button class="ordenizer" type="submit">Order</button>
    </form>
    <ul class="courses" id="mix-wrapper">
       <li class="mix-target" v-for="n in displaying" v-bind:data-order="n">
          <span>{{n}}</span>
       </li>
    </ul>
  </div>
</template>

<script>
require('mixitup');

export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to El Comercio Sort Assessment',
      number: 0,
    };
  },
  computed: {
    displaying() {
      return this.number.toString().split('');
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
  font-size: 3rem;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

form {
  display: flex;
  flex: 1 0;
  justify-content: center;
}

#inputNumber {
  background: rgba(128, 128, 128, 0.13);
  font-size: 24px;
  height: 3rem;
  border: none;
}
button.ordenizer {
  background: #fbbe00;
  border: 0;
  padding: 1rem;
  margin: 0;
  font-size: 14px;
  letter-spacing: 1px;
  font-weight: 600;
  border-radius: 4px;
  cursor: pointer;
}
</style>
