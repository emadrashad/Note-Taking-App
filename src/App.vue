<template>
  <div id="app" class="container">
    <img alt="Vue logo" src="./assets/logo.png">


      <div class="notes-section">
        <div class="columns">
          <div class="column  has-text-centered">
            <strong class="title">Notes</strong>
            <div class="notes">
              <h3 class="the_note" v-for="(note,index) in notes" v-bind:key="index">
                  {{ note }}
              </h3>
            </div>
          </div>
          <div class="column has-text-centered">
            <strong>Timestamp</strong>
             <div class="timestamps">
              <h3 class="the_timestamp" v-for="(stamp,index) in timestamp" v-bind:key="index">
                  {{ stamp }}
              </h3>
            </div>
          </div>
        </div>
        <NoteEntry 
            :plc="plc"
            />

        <NotesCount /> 
      </div>
    
  </div>
</template>

<script>
 
import NoteEntry from './components/NoteEntry.vue' ; 
import NotesCount from './components/NotesCount.vue' ; 

import {EventBus} from './Event.js' ; 

export default {
  name: 'app',
  components:{
    NoteEntry,
    NotesCount
  }, 
  data(){
    return {
      notes : [] , 
      timestamp : [],
      plc:'write down your note eaisly'
    }
  }, 
  created(){
    EventBus.$on('add-note' , event => this.addNoteFun(event));
  },
  methods:{
    addNoteFun(event){
      this.notes.push(event.data.note);
      this.timestamp.push(event.data.timestamp);
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

.the_note{
 
  color: blue;
}

.title{
  font-size: 30px; 
}
</style>
