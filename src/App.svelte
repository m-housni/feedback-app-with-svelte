<script>
	import FeedbackList from './components/FeedbackList.svelte'
	import FeedbackForm from './components/FeedbackForm.svelte'
  import Card from './components/Card.svelte'


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
  
  <FeedbackForm />
  
  {#if count }
  <div class="space-around">
    <div class="float-left">
      <span class="badge">{count}</span>
    </div>
    <div class="float-right">
      <span class="badge">{avg.rating / count}</span>
    </div>
  </div>
  {/if}
  
	<FeedbackList feedback="{feedback}" on:delete-feedback={deleteFeedback}/> 
	<!-- 
		Equivalent to: 
		<FeedbackList {feedback} /> 
	 -->
</main>

<style>

</style>