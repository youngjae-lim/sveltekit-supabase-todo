<script>
  import supabase from "$lib/db";
  import Todo from "$lib/Todo.svelte";
  import { onMount } from "svelte";

  let todos = [];

  onMount(async () => {
    let { data, error } = await supabase.from("todos").select("*");
    todos = data;
    console.table(todos);
  });

  const updateTodo = async (todo) => {
    try {
      const { data, error } = await supabase
        .from("todos")
        .update({ task: todo.task })
        .eq("id", todo.id);
    } catch (err) {
      console.log(err);
    }
  };
</script>

{#each todos as todo}
  <Todo {todo} {updateTodo} />
{:else}
  <p>No todos found</p>
{/each}
