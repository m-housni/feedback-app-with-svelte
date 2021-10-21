<script>
	import FeedbackItem from './FeedbackItem.svelte'

  export let feedback = []
  console.log(feedback)

  // reactive value
  $: count = feedback.length 
  $: avg = feedback.length ? feedback.reduce((prev, cur) => { return {rating: prev.rating+cur.rating}}) : {}

</script>

<main>

  {#if count }
  <div class="space-around">
    <div class="float-left">
      <span class="badge">{count} {count == 1 ? 'feedback' : 'feedbacks'}</span>
    </div>
    <div class="float-right">
      <span class="badge">{avg.rating / count}/10</span>
    </div>
  </div>
  {/if}

  {#each feedback as fb (fb.id)}
    <FeedbackItem {fb}  on:delete-feedback/>
  {/each}
</main>

<style>
  .space-around {
    padding-bottom: 30px;;
    padding-left: 20px;
    padding-right: 20px;
  }
  .badge {
    color: #fff;
  }
</style>