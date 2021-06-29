<template>
  <header id="todoheader">
    <h1>TODO APP</h1>
    <form @submit.prevent="addItem">
      <input type="text" name="newitem" id="newitem" v-model="itemTitle" placeholder="Add to the todo list">
      <button id="additem" type="submit">Add item</button>
    </form>
  </header>
  <main id="todolist">
    <div v-if="items.length">
      <ul>
        <li v-for="(item, index) in items" :key="index" :class="{'done' : item.done}" >
          <span class="label" @click="changeItemStatus(index)">{{item.title}}</span>
          <button type="button" aria-label="Delete" title="Delete" @click="deleteItem(index)">
            <i class="fas fa-trash-alt fa-3x"></i>
          </button>
        </li>
      </ul>
    </div>
    <p class="emptylist" v-else>Your todo list is empty.</p>
  </main>
</template>

<script>
  const localKey = 'todos';
    export default {
        data() {
            return {
                itemTitle: '',
                items: [],
            }
        },
        methods: {
            addItem() {
                if (!this.itemTitle) {
                    return;
                }
                this.items.push({
                    title: this.itemTitle,
                    done: false,
                });
                this.itemTitle = '';
            },
            deleteItem(index) {
                this.items.splice(index, 1);
            },
            changeItemStatus(index) {
                const item = this.items[index];
                this.items[index].done = !item.done;
            }
        },
        mounted() {
            const items = localStorage.getItem(localKey) || '[]';
            this.items = JSON.parse(items);
        },
        watch: {
            items: {
                deep: true,
                handler(items) {
                    localStorage.setItem(localKey, JSON.stringify(items))
                }
            }
        }
    }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html, body {
      background: #8d99ae;
      font-size: 1.1rem;
      font-family: 'Noto Sans JP', sans-serif;
      height: 100%;
  }

  #todoheader {
    height: 15rem;
    background: #2b2d42;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    color: #85182a;
    border-radius: 0 0 1rem 1rem;
  }

  #todoheader h1 {
    font-size: 3rem;
  }

  #todoheader form {
    margin: 2rem 0;
    display: flex;
    justify-content: center;
    width: 100%;
  }

  #newitem {
    border: 0.1rem solid #8d99ae;
    outline: none;
    width: 40%;
    padding: 0.8rem;
    background: #dee2e6;
    color: #85182a;
    border-radius: 2rem 0 0 2rem;
  }

  #newitem:hover{
    background: #adb5bd;
    transition: 0.3s;
  }

  #newitem::placeholder {
    color: #85182a;
  }

  #additem {
    border: 0.1rem solid #8d99ae;
    border-left: none;
    background: #dee2e6;
    color: #85182a;
    border-radius:  0 2rem 2rem 0;
    padding: 0 0.8rem;
    cursor: pointer;
  }

  #additem:hover{
    background: #adb5bd;
    transition: 0.3s;
  }

  #todolist {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  #todolist div {
    width: 100%;
  }

  #todolist ul {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
  }

  #todolist li {
    width: 50%;
    display: flex;
    margin: 0 -3rem 4px;
    padding: 1.1rem 3rem;
    justify-content: space-between;
    align-items: center;
    border-bottom: 0.2rem solid #2b2d42;
    border-radius: 0 0 1rem 1rem;
    color: #dee2e6;
  }

  #todolist button {
    background: none;
    border: none;
    cursor: pointer;
    color: #85182a;
    transition: 0.3s;
  }

  #todolist button:hover {
    color: #520814;
  }

  #todolist .label {
    position: relative;
    transition: opacity .2s linear;
    cursor: pointer;
    transition: 0.3s;
  }

  #todolist .label:hover {
    color: #6c757d;
  }

  #todolist .done .label {
    opacity: .6;
    text-decoration: line-through;
    color: #343a40;
  }
  
  #todolist .done .label:before {
    content: '';
    position: absolute;
    top: 50%;
    left: -.5rem;
    display: block;
    width: 0%;
    height: 1px;
    background: #ddd;
    animation: strike .3s ease-out 0s forwards;
  }

  .emptylist {
    padding: 3rem;
    font-size: 1.5rem;
    color: #dee2e6;
  }
</style>