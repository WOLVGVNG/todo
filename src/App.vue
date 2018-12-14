<template>
  <div id="app">
    <h1>THINGS TO DO:</h1>
    <div class='row form-group mt-5'>
        <input type='text' @keyup.enter="addItem" v-model='value' class='col-10 col-md-4 mx-auto p-2 border' />
        <div class='w-100' />
        <button @click='addItem' class='col-2 col-md-1 mx-auto mt-4 btn btn-dark' type=button>Add
        </button>
    </div>
        <div class='w-100'></div>
        <br>
         <ul class='col-11 col-sm-10 col-md-7 col-xl-5 list-unstyled mx-auto' v-for='Item in Items' :key='Item.id'>
           <li v-if="Item.value!=''">
             <div class='row py-2'>
              <button type='button' class='col-2 col-l-1 btn btn-outline-dark btn-sm' @click='deleteItem(Item.id)'>Delete</button>
              <button type='button' class='col-2 col-l-1 btn btn-outline-dark btn-sm' @click='changeState(Item.id)'>Done</button>
              <p class='col-7 col-l-9 mt-3 text-center' :class='{done: Item.done}'>{{ Item.value }}</p>
            </div>
            <hr>
           </li>
         </ul>
    </div>
</template>

<script>
let i = 0;
let value;

export default {
  name: 'app',
  data() {
    return {
      id: '',
      value: '',
      Items: [],
    };
  },
  methods: {
    addItem() {
      if (this.value !== '') {
        this.Items[i] = { 
          id: i,
          value: this.value,
          done: false
          };
        i += 1;
        this.value = '';
      }
    },
    deleteItem(id) {
      this.Items[id] = { id: id, value: '' };
      value = this.value;
      this.value = 'update';
      this.value = value;
    },
    changeState(id) {
      if (this.Items[id].done === true) this.Items[id].done = false;
      else this.Items[id].done = true;
      value = this.value;
      this.value = 'update';
      this.value = value;
    },
  },
};
</script>

<style lang="scss">
  @import '../node_modules/bootstrap/scss/bootstrap.scss';

  h1 {
    text-align: center;
    margin: 20px 0;
  }
  textarea {
    height: 30vh;
  }

  p {
    overflow: auto;
  }

  ul {
    min-height: 0px;
    margin: 0px;
  }

  .done {
    text-decoration: line-through;
    color: silver;
  }

  .btn {
    max-height: 32px;
    margin-top: 11px;

    @media (max-width: 400px) {
      font-size: 10px;
    }
  }

  button:first-child {
    margin-right: 4px;
  }
</style>
