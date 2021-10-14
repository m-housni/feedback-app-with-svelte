<script>
  export let feedback = []
  console.log(feedback)
</script>

<main>
  {#each feedback as fb (fb.id)}
    <h3>{fb.text}</h3>
  {/each}
</main>

<style>

</style>