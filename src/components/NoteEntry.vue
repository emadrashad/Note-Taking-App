<template>

    <div id="note_entry" class="container">

        <p></p>
         <div class="column">
            <input type="text" class="input" 
                    v-model="noteEntry" 
                    :placeholder='plc'
                    @keyup.enter="monitorEnterKey"/>

        <p style="color: red; font-size: 13px" v-if="error" >
                You must type something first!
        </p>
        </div>
         

    </div>

</template>

<script>

import {EventBus} from '../Event.js' ; 

export default {
    name : 'NoteEntry', 
    props : ['plc'] , 
    data(){
        return {
            noteEntry : '',
            error:false 
        }
    },
    methods:{
        monitorEnterKey(){
             this.noteEntry === '' ? this.error = true : this.error = false ; 
             if(this.error == true)
             return false ; 
             
             EventBus.$emit('add-note' , {

                 data : {
                     note : this.noteEntry , 
                     timestamp : new Date().toLocaleTimeString()
                 }
             });

             this.noteEntry = ''; 
        }
    }
   
}
</script>

<style scoped>


 
</style>
