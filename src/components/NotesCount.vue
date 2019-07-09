<template>
    
    <div class="container">
           <p>Notes count : <strong>{{ noteCount }}</strong></p>
    </div>
 
    

</template>

<script>

import {EventBus} from '../Event.js' ; 

export default {
    name : 'NotesCount', 
    data(){
        return {
            noteCount:0
        }
    },
    created(){
        EventBus.$on('add-note' , event => this.noteCount++) ; 
    }
}
</script>

<style scoped>

</style>
