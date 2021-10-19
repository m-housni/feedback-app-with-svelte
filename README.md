# Feedback App with Svelte

In this project we will learn the basics of the Svelte  framework.

## Create New App

```
npx degit sveltejs/template feedback-app
```
## Install the dependencies

```
npm i
```

## Build the project on dev mode

```
npm run dev
```

## Clean the starter
- src/App.svelte
- src/main.js
## Create a feedback variable as an array of objects like:
```
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
```
## Create a feedbackList and feedbackItem components 
![](/assets/img1.png)

## Pass the feedback variable to the FeedbackList component
- App
```
<main>
	<FeedbackList feedback="{feedback}" /> 
	<!-- 
		Equivalent to: 
		<FeedbackList {feedback} /> 
	 -->
	
</main>
```
- FeedbackList
```
<script>
  export let feedback = []
  console.log(feedback)
</script>
```

## Loop and render the feedbacks
- FeedbackList
```
<main>
  {#each feedback as fb (fb.id)}
    <h3>{fb.text}</h3>
  {/each}
</main>
```

## Wrap the feedback in FeedBackItem and style it within Card component
- FeedBackItem
```
<script>
  import Card from './Card.svelte'
  export let fb = ''
</script>   

<Card>
  <p>Card</p>
</Card>
```
- Card
```
<div class="card">
  <slot></slot>
</div>

<style>
  .card {
    padding: 15px;
    margin: 15px;
    border-radius: 15px;
    color: #fff;
    background-color: purple;
    position: relative;
  }
</style>
```
![](/assets/img2.png)
## Style the card elements 
- FeedbackItem.svelte
```
<script>
  import Card from './Card.svelte'
  export let fb = ''
</script>   

<Card>
  <div class="num-display">
    {fb.rating}
  </div>
  <div class="close">
    x
  </div>
  <div class="text-display">
    {fb.text}
  </div>
</Card>

<style>
  .num-display {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 35px;
    height: 35px;
    background: #fff;
    color: #000;
    border: 1px #000 solid;
    border-radius: 50%;
    padding: 10px;
    text-align: center;
    font-size: 25px;
  }

  .close {
    positi![](2021-10-19-11-53-25.png)on: absolute;
    top: 10px;
    right:20px;
    cursor: pointer;
  }
</style>
```
![](/assets/img3.png)

## Delete a feedback
- feedbackItem
```
<script>
  import {createEventDispatcher} from 'svelte'
  import Card from './Card.svelte'
  export let fb = ''

  const dispatch = createEventDispatcher()

  const handleDelete = (fbId) => {
    dispatch('delete-feedback', fbId)
  }

</script>   

<Card>
  <div class="num-display">
    {fb.rating}<sub style="font-size:.8rem">/10</sub>
  </div>
  <div class="close" on:click={() => handleDelete(fb.id)}>
    x
  </div>
  <div class="text-display">
    {fb.text}
  </div>
</Card>
```
- feedbackList
```
<main>
  {#each feedback as fb (fb.id)}
    <FeedbackItem {fb}  on:delete-feedback/>
  {/each}
</main>
```
- App
```
<script>
	import FeedbackList from './components/FeedbackList.svelte'
	let feedback = [
    {
      id: 1,
      rating: 5,
      text: "rating text 1"
    },
    ...
  ]

  const deleteFeedback = (e) => {
    const fbId = e.detail
    feedback = feedback.filter((fb) => {
      return fb.id != fbId
    })
  }
</script>

<main class="container">
	<FeedbackList feedback="{feedback}" on:delete-feedback={deleteFeedback}/> 
	<!-- 
		Equivalent to: 
		<FeedbackList {feedback} /> 
	 -->
</main>
```
## Show feedbacks number and average
- App
```
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
```