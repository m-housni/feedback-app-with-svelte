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
]
</script>

<main>
	<FeedbackList/>
</main>

<style>

</style>