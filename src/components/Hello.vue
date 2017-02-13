<template>
  <div class="hello">
    <h1>Welcome to El Comercio Sort Assessment</h1>
    <h2>Bellow put some number to sort:</h2>
    <form class="form" @submit.prevent="sorting">
      <input type="text" pattern="[0-9]*" name="inputNumber" id="inputNumber" v-model="number"/>
      <button class="sort-btn" type="submit" v-bind:disabled="flag">Order</button>
    </form>
    <p class="error" v-show="msg">{{msg}}</p>
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
      number: 0,
      ref: null,
      array: [],
      flag: false,
      msg: null,
    };
  },
  computed: {
    /* Nomber's watcher to split it and validate no-repeat elements each time
     * the input number is modified and update the <ul> tag. If one or more
     * elemets are duplicated we show a message error and disabled form.
     */
    displaying() {
      this.array = this.number.toString().split('');
      const repeats = this.showDuplicates(this.countElems());
      if (repeats.length > 0) {
        this.flag = true;
        this.msg = `The element(s) ${repeats} are duplicates. Please remove it`;
      } else {
        this.flag = false;
        this.msg = null;
      }
      return this.array;
    },
  },
  methods: {
    /* Sorting function
     * Details: We bind the number list with the mixitup library object, if the
     * bind exist before it's destroyed to re-bind the dataset.
     */
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
    /*
     * Method to create a json with the number of times a element is there
     */
    countElems() {
      return this.array.reduce((a, b) => Object.assign(a, { [b]: (a[b] || 0) + 1 }), {});
    },
    /*
     * Method to return what elements are duplicates
     */
    showDuplicates(obj) {
      return Object.keys(obj).filter(a => obj[a] > 1);
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

.hello {
  max-width: 30rem;
  margin: 0 auto;
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
.error {
  background: orangered;
  color: #fff;
  font-size: 17px;
  font-weight: 600;
}
</style>
