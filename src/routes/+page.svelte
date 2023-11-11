<!-- <script context="module" lang="ts">
    export { load } from './+page.server';
  </script>
  
  <script>
    export let data; // Los datos del servidor estarán disponibles aquí
  </script> -->

<script>
    let new_todo;
    let todos = [];
    
    const addTodo = (e) => {
        todos = [
            ...todos,
            {
                id: todos.length + 1,
                text: new_todo,
                checked: false,
            },
        ];
        e.target.reset();
    };
    
    const removeTodo = (id) => {
        todos = todos.filter((t) => t.id !== id);
    };
</script>

<form on:submit|preventDefault={addTodo}>
    <input type="text" bind:value={new_todo} autocomplete="off" />
    <button type="submit">Añadir</button>
</form>

<ul>
    {#each todos as todo}
        <li>
            <form on:submit|preventDefault={() => removeTodo(todo.id)}>
                <input 
                   type="checkbox"
                   name={todo.id} 
                   id={todo.id}
                   bind:checked={todo.checked}
                />
                <label for={todo.id}>{todo.text}</label>
                <button type="submit">Borrar</button>
            </form>
        </li>
    {/each}
</ul>

<style>
    form,
    ul {
        margin: 20px;
        background-color: #f4f4f4;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /*incorporar sombras*/
    }

    input,
    button {
        margin-bottom: 10px;
    }

    input {
        padding: 8px;
        border: 1px solid #a3979a;
        border-radius: 4px;
    }

    input:checked {
        background-color: rgb(0, 139, 120);
        border: 1px solid rgb(0, 139, 120);
        color: white;
    }

    button {
        padding: 8px;
        background-color: rgb(0, 139, 120);
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    button:hover {
        background-color: #007d68;
    }

    input:checked + label {
        text-decoration: line-through;
    }

    ul {
        list-style: none;
        padding: 0;
    }

    li {
        margin-bottom: 10px;
    }

    :global(body) {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 16px;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;

    /* transition: background-color 0.3s ease, color 0.3s ease, border 0.3s ease; */

}
</style>

