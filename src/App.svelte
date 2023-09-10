<script>
  import Board from "./Board.svelte";
  let columnsData = [
    {
      id: "c1",
      name: "TODO",
      items: [
        { id: 1, name: "item41", details: "Task 41 Details" },
        { id: 2, name: "item42", details: "Task 42 Details" },
        { id: 3, name: "item43", details: "Task 43 Details" },
        { id: 4, name: "item44", details: "Task 44 Details" },
        { id: 5, name: "item45", details: "Task 45 Details" },
        { id: 6, name: "item46", details: "Task 46 Details" },
        { id: 7, name: "item47", details: "Task 47 Details" },
        { id: 8, name: "item48", details: "Task 48 Details" },
        { id: 9, name: "item49", details: "Task 49 Details" },
      ],
    },
    {
      id: "c2",
      name: "DOING",
      items: [
        { id: 10, name: "item50", details: "Task 50 Details" },
        { id: 11, name: "item51", details: "Task 51 Details" },
      ],
    },
    {
      id: "c3",
      name: "DONE",
      items: [{ id: 13, name: "item52", details: "Task 52 Details" }],
    },
  ];
  function handleBoardUpdated(newColumnsData) {
    columnsData = newColumnsData;
  }
</script>

<center>
  <h2>Board</h2>

  <br />
  <hr />
  <br />

  <Board columns={columnsData} onFinalUpdate={handleBoardUpdated} />
</center>

<style>
  :global(*) {
    box-sizing: border-box;
    margin: 0;
  }
</style>
