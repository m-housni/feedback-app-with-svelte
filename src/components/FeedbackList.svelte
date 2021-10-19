<script>
	import FeedbackItem from './FeedbackItem.svelte'

  export let feedback = []
  console.log(feedback)
</script>

<main>
  {#each feedback as fb (fb.id)}
    <FeedbackItem {fb}  on:delete-feedback/>
  {/each}
</main>

<style>

</style>