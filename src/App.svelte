<script>
 import Dashboard from "./components/Dashboard.svelte";
 import Header from "./components/Header.svelte";
 import {v4} from 'uuid';
 import { darkmode } from './store/store.js';


 let notes =[
   {
      id: 0,
	  title: 'Vacaciones',
	  color: '#DDFFC2',
      text: 'Hola!',
    },
    {
      id: 1,
	  title: 'Tareas',
	  color: 'skyblue',
      text: 'Hola!',
    },
];
let copyNotes = [...notes];

$: count = notes.length;

function handleNew(){
   const color = generateColor();
   const id = v4();
   const note = {
      id: id,
      title: '',
      color: color,
      text: ''
   };
   notes = [note, ...notes];
   copyNotes = [...notes];
}
function generateColor(){
   const colors = ['#DDFFC2','#FFC2C2','#FFEAC2','#C2FFD3','#C2FFEC','#C2FAFF','#CBC2FF','#EBC2FF','#FFC2F7','#C2E2FF','#EBC2FF','#FFC2F7','#FFC2D8','skyblue']
   const index = Math.floor(Math.random() * (colors.length));
   return colors[index];
}
function handleUpdate(e){
const note = e.detail;
const index= notes.findIndex(n => n.id === note.id);
notes[index]= note;
copyNotes = [...notes];
}
function handleColor(e){
const index= notes.findIndex(n => n.id === e.detail.id);
notes[index].color = generateColor();
copyNotes[index].color = notes[index].color;
}
function handleRemove(e){
const response = notes.filter( n => n.id != e.detail.id);
notes = [...response];
copyNotes = [...notes];
}
function handleSearch(e){
   const q = e.target.value;

   if(q === ''){
      copyNotes = [...notes];
      return false;
   }
   
   const results = notes.filter(note => {
      const title = note.title.toLowerCase();
      const text = note.text.toLowerCase();

      return title.indexOf(q) > -1 || text.indexOf(q) > -1;
   });
   copyNotes = [...results];
}
</script>

<main class={$darkmode? 'darkmode' : ''}>
   <Header on:input={handleSearch}/>
   <div class="count-notes">{count} notas</div>
   <Dashboard 
   bind:notes={copyNotes}
   on:click={handleNew} 
   on:update={handleUpdate} 
   on:color={handleColor} 
   on:remove={handleRemove}/>
</main>

<style>
  :global(body){
   margin: 0;
   padding: 0;
   height: 100%;
  }

  main{
   height: 100%;
  }
  
  :global(main.darkmode, main.darkmode textarea, main.darkmode input){
   background-color: #000;
   color: white;
  }
  .count-notes{
      padding: 20px 20px 0px 20px;
      text-align: right;
   }
</style>