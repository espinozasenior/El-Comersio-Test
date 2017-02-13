<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Bellow put some number to sort:</h2>
    <div class="form">
      <input type="text" pattern="[0-9]*" name="inputNumber" id="inputNumber" v-model="number"/>
      <button class="sort-btn" v-on:click="sorting">Order</button>
    </div>
    <ul class="courses" id="mix-wrapper">
      <li class="mix-target undergraduate" v-for="n in displaying" v-bind:data-order="n"><span>{{n}}</span></li>
    </ul>
  </div>
</template>

<script>
import mixitup from 'mixitup';

export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to El Comercio Sort Assessment',
      number: 0,
      ref: null,
    };
  },
  computed: {
    displaying() {
      return this.number.toString().split('');
    },
  },
  methods: {
    sorting() {
      if (this.ref !== null) {
        this.ref.destroy();
      }
      this.ref = mixitup('#mix-wrapper', {
        animation: {
          effects: 'fade rotateZ(-180deg)',
          duration: 700,
        },
        classNames: {
          elementSort: 'sort-btn',
        },
        selectors: {
          target: '.mix-target',
        },
      });
      this.ref.sort('order:asc');
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

.form {
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
button.sort-btn {
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
