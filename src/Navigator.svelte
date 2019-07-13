<script>
  import { createEventDispatcher } from "svelte";

  export let currentPage;
  let page;

  // dispatcher to emit events, which are 'prev' and 'next'
  const dispatch = createEventDispatcher();

  // go back 1 page
  function prev() {
    dispatch("prev");
  }

  // go forward 1 page
  function next() {
    dispatch("next");
  }

  // go to specific page
  function go(ev) {
    if (ev.keyCode === 13) {
      // pressed enter
      dispatch("go", {
        page
      });
    }
  }
</script>

<style>
  div {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  button {
    all: unset;
    box-sizing: border-box;
    padding: 4px 24px;
    color: teal;
    outline: 1px solid teal;
    margin-right: 8px;
  }
  button:hover {
    opacity: 0.6;
    cursor: pointer;
  }
  button:disabled {
    opacity: 0.4;
  }
  input {
    all: unset;
    box-sizing: border-box;
    padding: 4px 8px;
    outline: 1px solid teal;
  }
</style>

<div>
  <button on:click={prev} disabled={currentPage === 1}>Previous</button>
  <button on:click={next}>Next</button>
  <input
    type="number"
    bind:value={page}
    placeholder="Go to page"
    on:keyup={go} />
</div>
