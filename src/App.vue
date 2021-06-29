<template>
  <header id="todoheader">
    <h1>TODO APP</h1>
    <form @submit.prevent="addItem">
      <input type="text" name="newitem" id="newitem" v-model="itemTitle" placeholder="Add to the todo list">
      <button id="additem" type="submit">Add item</button>
    </form>
  </header>
  <main id="todolist">
    
  </main>
</template>

<script>

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
    color: #d90429;
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
    color: #d90429;
    border-radius: 2rem 0 0 2rem;
  }

  #newitem:hover{
    background: #adb5bd;
    transition: 0.3s;
  }

  #newitem::placeholder {
    color: #d90429;
  }

  #additem {
    border: 0.1rem solid #8d99ae;
    border-left: none;
    background: #dee2e6;
    color: #d90429;
    border-radius:  0 2rem 2rem 0;
    padding: 0 0.8rem;
    cursor: pointer;
  }

  #additem:hover{
    background: #adb5bd;
    transition: 0.3s;
  }
</style>