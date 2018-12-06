<template>
  <div id="app" class="container">
    <div class="page-header">
    <h1>vue.js & Firebase</h1>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Add Book</h3>
      </div>
      <div class="panel-body">
        <form id="form" class="form-inline" v-on:submit.prevent="addBook">
          <div class="form-group">
            <label for="bookTitle">Title:</label>
            <input type="text" id="bookTitle" class="form-control" v-model="newBook.title">
            </div>
              <div class="form-group">
            <label for="bookAuthor">Author:</label>
            <input type="text" id="bookAuthor" class="form-control" v-model="newBook.Author">
            </div>
              <div class="form-group">
            <label for="bookUrl">Url:</label>
            <input type="text" id="bookUrl" class="form-control" v-model="newBook.url">
            </div>
            <br>

            <input type="submit" class="btn btn-primary" value="Add Book">
            
        </form>
      </div>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Books Lists</h3>
      </div>
       <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Title
              </th>
              <th>
                Author
              </th>
              <th>
                Delete
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books">
              <td>
               <a v-bind:href="book.url">{{book.title}}</a>
              </td>
              <td>
                {{book.Author}}
              </td>
              <td>
                 <span class="glyphicon glyphicon-trash" aria-hidden="true" v-on:click="removeBook(book)">delete</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      </div>
            
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Firebase from 'firebase'
let config = {

    apiKey: "AIzaSyC98ZNt51dpGk4TOZxsghrDJk-KoxySJKE",
    authDomain: "vuejs-firebase-00.firebaseapp.com",
    databaseURL: "https://vuejs-firebase-00.firebaseio.com",
    projectId: "vuejs-firebase-00",
    storageBucket: "vuejs-firebase-00.appspot.com",
    messagingSenderId: "973607686388"
}
let app = Firebase.initializeApp(config);
let db = app.database();

let booksRef = db.ref('books');
export default {
  name: 'App',
  firebase: {
     books: booksRef

  },
  data () {
    return {
      newBook: {
        title: '',
        author: '',
        url: ''
      }
    }
  },
  methods: {
    addBook: function(){
      booksRef.push(this.newBook);
      this.newBook.title = '';
      this.newBook.author = '';
      this.newBook.url = '';

    },
    removeBook: function(book){
      booksRef.child(book['.key']).remove();
    }
  }
 }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
