<script>
   import Logo from "./Logo.svelte";
   import Search from "./Search.svelte"; 
   import Settings from "./Settings.svelte";
   import Switch from "./Switch.svelte";
</script>

<div class="Header">
   <Logo appName='Notas'/>
   
   <Search on:input/>
   
   <Settings />

   <Switch/>

</div>

<style>
    .Header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        align-content: center;
        border-bottom: solid 1px #ccc;
        padding: 10px;
        
    }

</style>