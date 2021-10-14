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
</script>

<main>
	<FeedbackList feedback="{feedback}" /> 
	<!-- 
		Equivalent to: 
		<FeedbackList {feedback} /> 
	 -->
	
</main>

<style>

</style>