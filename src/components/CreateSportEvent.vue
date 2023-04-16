 
<template>
<div>
        
  <ListEvents :events="events" type="Sportifs"/>     
 <div v-if="isAddEventAllowed"> 
    <h4 class="text-center"> Ajouter un autre evenment sportif </h4>
    
    <form>
    <div class="d-flex justify-content-between">
     <div class="form-group">
            <label class="text-center text-bold" >Titre de l'evenment</label>
            <input class="form-control" type="text" v-model="title">
    
    </div>
         <br/>

          <div class="form-group">
            <label class="text-center text-bold">Description de l'evenment</label>
            <textarea class="form-control" cols="25" rows="10" v-model="description"></textarea>
        </div>
        <br/>
    

        <div class="form-group">
            <label class="text-center text-bold" >Date de l'evenment </label>
            <input class="form-control" type="date" v-model="date">
        </div>
        <br/>

      

         <div class="form-group">
           <label class="text-center text-bold"> Quelles Sports souheterai vous jouer? </label>
        <VueMultiSelect
            v-model="selectedSports"
            :options="optionsSports"
            :multiple="true"
            placeholder="Choisir vos sports"
            label="name"
            track-by="name"
            :close-on-select="false"
            >
            
        </VueMultiSelect>
         </div>
     </div>
     <br/>
        <div class="d-flex justify-content-center">
            <button @click="addSportingEvent" type="submit" class="btn btn-primary w-50">Submit</button>
        </div>
    </form> 
 
</div>

<div v-else>
    <h4 class="text-danger text-center"> La limité d'evenments est attient </h4>
</div>

</div>

        
    
</template>

<script>

import  VueMultiSelect from 'vue-multiselect';
import ListEvents from "./ListEvents.vue"
export default {
    name:"CreateSportEvent",
    components:{VueMultiSelect,ListEvents},
    data(){
        return {
            events:[],
            title:"",
            description:"",
            date:null,
            selectedOptions:[],
            options:[{name:"Tennis"},{name:"Kitesurf"},{name:"Golf"},{name:"Surf"},{name:"Football"},{name:"Basketabll"}],
            maximumAllowedEvents:5
        }
    },


    computed:{
        isAddEventAllowed(){
            
            return this.events.length<this.maximumAllowedEvents;
        },

        isEventsExists(){
            return this.events.length>0
        },
    },

    methods:{
        addEvent(event){
            event.preventDefault();
            const eventsCopy=[...this.events];
            eventsCopy.push({title:this.title,description:this.description,activites:this.selectedOptions,date:this.date});
            this.events=eventsCopy;
            this.clearData();
        },

        clearData(){
            this.title="";
            this.description="";
            this.date=null;
            this.selectedSports=[];
        }
    }

    

}
</script>

<style src="vue-multiselect/dist/vue-multiselect.css"></style>
<style scoped>
    .text-bold{
        font-weight:bold;
    }
</style>


