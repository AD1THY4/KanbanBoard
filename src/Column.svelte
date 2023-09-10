<script>
  import { flip } from "svelte/animate";
  import { dndzone } from "svelte-dnd-action";
  const flipDurationMs = 150;
  export let name;
  export let items;
  export let onDrop;

  function handleDndConsiderCards(e) {
    console.warn("got consider", name);
    items = e.detail.items;
  }
  function handleDndFinalizeCards(e) {
    onDrop(e.detail.items);
  }
</script>

<div class="wrapper">
  <div class="column-title">
    {name}
  </div>
  <div
    class="column-content"
    use:dndzone={{ items, flipDurationMs, zoneTabIndex: -1 }}
    on:consider={handleDndConsiderCards}
    on:finalize={handleDndFinalizeCards}
  >
    {#each items as item (item.id)}
      <div class="card" animate:flip={{ duration: flipDurationMs }}>
        {item.name}
        <br />

        {item.details}
      </div>
    {/each}
  </div>
</div>

<style>
  .wrapper {
    height: 100%;
    width: 100%;
    overflow-y: hidden;
  }
  .column-content {
    height: calc(100% - 2.5em);
    overflow-y: scroll;
  }
  .column-title {
    height: 2.5em;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .card {
    height: 4em;
    width: 100%;
    margin: 0.4em 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #dddddd;
    border: 1px solid #333333;
  }
</style>
