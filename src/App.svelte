<script>
	import FeedbackList from './components/FeedbackList.svelte'
	let feedback = [
    {
      id: 1,
      rating: 5,
      text: "rating text 1"
    },
    {
      id: 2,
      rating: 6,
      text: "rating text 2"
    },
    {
      id: 3,
      rating: 7,
      text: "rating text 3"
    },
    {
      id: 4,
      rating: 7,
      text: "rating text 4"
    },
  ]
  let list = [5,2,2]
  // reactive value
  $: count = feedback.length 
  $: avg = feedback.length ? feedback.reduce((prev, cur) => { return {rating: prev.rating+cur.rating}}) : {}

  const deleteFeedback = (e) => {
    const fbId = e.detail
    feedback = feedback.filter((fb) => {
      return fb.id != fbId
    })
  }
</script>

<main class="container">
  <h1>Feedbacks: {count}</h1>
  {#if feedback.length}<h1>Average: {avg.rating/feedback.length}</h1> {/if}
	<FeedbackList feedback="{feedback}" on:delete-feedback={deleteFeedback}/> 
	<!-- 
		Equivalent to: 
		<FeedbackList {feedback} /> 
	 -->
</main>

<style>

</style>