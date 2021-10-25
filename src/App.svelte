<script>

  // import components
	import FeedbackList from './components/FeedbackList.svelte'
	import FeedbackForm from './components/FeedbackForm.svelte'
  import Card from './components/Card.svelte'

	$: feedback = [
    // store the feedbacks in an array of objects
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

  const deleteFeedback = (e) => {
    // arrow function to delete a feedback
    const fbId = e.detail
    feedback = feedback.filter((fb) => {
      return fb.id != fbId
    })
  }

  const handleNewFeedback = (e) => {
    // arrow function to add new feedback
    /*
      the dispatched event comes with a detail property that bears the value
      ... is the spread operator:
      EXAMPLE:
      let numberStore = [0, 1, 2]
      let newNumber = 12
      numberStore = [...numberStore, newNumber]
      console.log(numberStore)
      // output: [0,1,2,12]
    */
    feedback = [e.detail, ... feedback] 
  }
</script>

<main class="container">

  <!-- Feedback form listening to new-feedback event -->
  <FeedbackForm on:new-feedback={handleNewFeedback} /> 

  <!-- 
    Feedback list listening to delete-feedback event 
    Tip: feedback="{feedback}" equivalent to {feedback}
  -->
	<FeedbackList 
    feedback="{feedback}" 
    on:delete-feedback={deleteFeedback}
  /> 
</main>

<style>
  .container {
    max-width: 768px;
    margin: auto;
  }
</style>