<script>
  export let picture;
</script>

<style>
  img {
    display: block;
    width: 100%;
  }
  a {
    display: inline-block;
    width: calc(100vw / 4 - 8px);
    padding: 4px;
  }
</style>

<a href={picture.url} title={`by ${picture.author}`}>
  <img src={picture.download_url} alt={picture.author} />
</a>
