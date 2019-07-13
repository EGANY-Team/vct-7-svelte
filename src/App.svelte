<script>
  import { onMount } from "svelte";
  import Navigator from "./Navigator.svelte";
  import PictureList from "./PictureList.svelte";

  let apiCall;
  let currentPage = 1;

  async function listByPage(page) {
    const res = await fetch(`https://picsum.photos/v2/list?page=${page}`);
    const result = await res.json();

    if (res.ok) {
      return result;
    } else throw new Error(result);
  }

  function goBack() {
    if (currentPage > 1) {
      const prevPage = currentPage - 1;

      currentPage = prevPage;
      apiCall = listByPage(prevPage);
    }
  }

  function goForward() {
    const nextPage = currentPage + 1;

    currentPage = nextPage;
    apiCall = listByPage(nextPage);
  }

  function goToPage(ev) {
    if (ev.detail.page > 0) {
      currentPage = ev.detail.page;
      apiCall = listByPage(ev.detail.page);
    }
  }

  onMount(() => {
    apiCall = listByPage(currentPage);
  });
</script>

<style>
  img {
    display: block;
    margin: 8px auto;
    max-width: 420px;
  }
</style>

<Navigator
  {currentPage}
  on:prev={goBack}
  on:next={goForward}
  on:go={goToPage} />

{#await apiCall}
  <img src="loading-cat.gif" alt="loading cat image" />
{:then result}
  <PictureList pictures={result} {currentPage} />
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
