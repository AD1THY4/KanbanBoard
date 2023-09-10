<script>
  import { flip } from "svelte/animate";
  import { dndzone } from "svelte-dnd-action";
  import Column from "./Column.svelte";
  // let tasks = [];

  // async function fetchTasks() {
  //   try {
  //     const response = await fetch('/api/tasks');
  //     const data = await response.json();
  //     tasks = data;
  //   } catch (error) {
  //     console.error('Error fetching tasks:', error);
  //   }
  // }

  // onMount(fetchTasks);
  const flipDurationMs = 300;

  export let columns;
  export let onFinalUpdate;

  function handleDndConsiderColumns(e) {
    columns = e.detail.items;
  }
  function handleDndFinalizeColumns(e) {
    onFinalUpdate(e.detail.items);
  }
  function handleItemFinalize(columnIdx, newItems) {
    columns[columnIdx].items = newItems;
    onFinalUpdate([...columns]);
  }
</script>

<section
  class="board"
  use:dndzone={{ items: columns, flipDurationMs, type: "column" }}
  on:consider={handleDndConsiderColumns}
  on:finalize={handleDndFinalizeColumns}
>
  {#each columns as { id, name, items }, idx (id)}
    <div class="column" animate:flip={{ duration: flipDurationMs }}>
      <Column
        {name}
        {items}
        onDrop={(newItems) => handleItemFinalize(idx, newItems)}
      />
    </div>
  {/each}
</section>

<style>
  .board {
    height: 100%;
    width: 100%;
    padding: 0.5em;
  }
  .column {
    height: 100%;
    width: 30%;
    padding: 0.5em;
    margin: 0.5em;
    float: left;
    border: 1px solid #333333;
  }
</style>
