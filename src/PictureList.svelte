<script>
  import PictureCapsule from "./PictureCapsule.svelte";

  export let pictures = [];
  export let currentPage;

  $: nFound = pictures ? pictures.length : 0;
</script>

<style>
  div {
    columns: 4;
  }
  h3 {
    margin: 8px;
    text-align: center;
  }
</style>

<h3>Showing {nFound} result{nFound > 1 ? 's' : ''} at page {currentPage}</h3>
<div>
  {#each pictures as picture (picture.id)}
    <PictureCapsule {picture} />
  {:else}
    <p>Wow much empty</p>
  {/each}
</div>
