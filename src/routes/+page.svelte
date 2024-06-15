<svelte:head>
    <title>
        ToDo List
    </title>
</svelte:head>

<script>
    let todos = [
        { id: 1, title: 'Learn Svelte', completed: true,editing: false},
        { id: 2, title: 'Learn Sapper', completed: false,editing: false},
        { id: 3, title: 'Learn SvelteKit', completed: false,editing:false },
    ];
    let textinput = ''

    function setEditing(i,isEditing){
        todos[i].editing = isEditing;
    }

    function DeleteTodo(i){
        todos.splice(i,1);
        todos = todos;
    }

    function AddTodo(){
        todos = [...todos,{id: todos.length + 1, title: textinput, completed: false,editing:false}]
        textinput = '';
    }
</script>
<main style="max-width: 100%;">
    
<div style="margin: 0 auto; padding: 20px;  display: flex; flex-direction: column; align-items:center;">
    <h2 style="font-size: 40px; font-weight: 600;">ToDo List</h2>
    <p style="font-weight: bold; ">Enter your todo here</p>

    <div>
        <input type="text" aria-label="todo input" bind:value={textinput}>
        <button on:click={AddTodo}>Add</button>
    </div>
  
</div>



<div style="display: flex; flex-direction:column; align-items:center; gap:10px; margin: 0 auto;">
   <div>
    {#each todos as todo,i}
    <div style="display: flex; flex-direction: row; align-items:center; gap: 10px;">
        {#if todo.editing}
        <input type="text" bind:value={todo.title}>
    {:else}
    <input type="checkbox" aria-label="checked" bind:checked={todo.completed}>
    <p>{todo.title}</p>
    {/if}
    <div style="display: flex;">
        {#if todo.editing}
            <button on:click={()=>setEditing(i,false)}>Save</button>
        {:else}
            <button on:click={()=>setEditing(i,true)}>Edit</button>
        {/if}
        <button on:click={()=>DeleteTodo(i)}>Delete</button>
    </div>
    </div>
    {/each}
   </div>
</div>
</main>



<style>
    h2 {
        text-align: center;
    }
    button{
        padding: 5px 10px;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        margin: 10px;
        font-size: 16px;
    }
    input{
        padding: 5px 10px;
        border: 1px solid #007bff;
        border-radius: 5px;
        font-size: 16px;
    }
    p {
        font-size: 20px;
        font-weight: bold;
    }
    input[type="checkbox"]{
        width: 20px;
        height: 20px;
      
    }
</style>