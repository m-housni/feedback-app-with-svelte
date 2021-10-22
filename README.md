# Feedback App with Svelte

In this project we will learn the basics of the Svelte framework.

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

```javascript
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

```html
<main>
	<FeedbackList feedback="{feedback}" />
	<!--
		Equivalent to:
		<FeedbackList {feedback} />
	 -->

</main>
```

- FeedbackList

```javascript
<script>
  export let feedback = []
  console.log(feedback)
</script>
```

## Loop and render the feedbacks

- FeedbackList

```html
<main>
  {#each feedback as fb (fb.id)}
    <h3>{fb.text}</h3>
  {/each}
</main>
```

## Wrap the feedback in FeedBackItem and style it within Card component

- FeedBackItem

```javascript
<script>
  import Card from './Card.svelte'
  export let fb = ''
</script>

<Card>
  <p>Card</p>
</Card>
```

- Card

```html
<div class="card">
  <slot></slot>
</div>

<style>
  .card {
    padding: 15px;
    margin: 15px;
    border-radius: 15px;
    color: #fff;
    background-color: #1E1D37;
    position: relative;
  }
</style>
```

![](/assets/img2.png)

## Style the card elements
- FeedbackItem.svelte
```javascript
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

```javascript
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

```html
<main>
  {#each feedback as fb (fb.id)}
    <FeedbackItem {fb}  on:delete-feedback/>
  {/each}
</main>
```

- App

```javascript
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

```javascript
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

## Add a feedback form
- FeedbackForm
```javascript
<script>
import {createEventDispatcher} from 'svelte'
const dispatch = createEventDispatcher()

import RatingSelect from './RatingSelect.svelte'
import {v4 as uuidv4} from 'uuid'
let btnDisabled = true, error = null
let rating = null
let text = ''

const handleInput = (e) => {
  let ln = e.target.value.trim().length
  if(ln>=10) {
    btnDisabled = false
    error = null
    text = e.target.value
  } else {
    btnDisabled = true
    error = 'Min 10 chars'
  }
}

const handleSelect = (e) => {
  rating = e.detail
}

const handleSubmit = () => {
  // validation
  if(!rating) {
    alert('Please rate!')
    return
  }

  // new feedback
  const newFeedback = {
    id: uuidv4(),
    text: text,
    rating: +rating
  }

  // push new feedback to feedbacks
  dispatch('new-feedback',newFeedback)
  text = ''
  
}

</script>

<form on:submit|preventDefault={handleSubmit}>
  <RatingSelect on:rating-select={handleSelect} />
  <div class="input-group text-center">
    <input type="text" value={text} placeholder="Feedback" on:input={handleInput}>
    <button type="submit" disabled={btnDisabled}>Send</button>
  </div>
  {#if error}
    <span class="error-badge">{error}</span>
  {/if}
</form>

<style>

  .error-badge {
    background: #fff;
    color: red;
    padding: 5px 15px;
    border: 1px #1E1D37 solid;
    border-radius: 10px;
    font-size:.8rem;
    margin-left: 10px;

  }

  form {
    background: #fff;
    padding: 50px 50px;
    margin: 15px;
    border-radius: 15px;
  }

  .input-group {
    border-radius: 15px;
    border: 1px lightgray solid;
    background: #fff;
  }

  input {
    min-width: 75%;
    border: none;
    margin: 0;
  }

  input:focus {
    outline: none;
  }

  button {
    padding: 5px 10px;
    font-size: 10px;
    border-radius: 10px;
    width: 20%;
  }
</style>
```
- RatingSelect
```javascript
<script>
import {createEventDispatcher} from 'svelte'
const dispatch = createEventDispatcher()
let ratings =  [1,2,3,4,5,6,7,8,9,10]

const onChange = (e) => {
  dispatch('rating-select', e.currentTarget.value)
}
</script>

<div class="radio-toolbar">
    {#each ratings as rating (rating)}
      <input type="radio" id="num{rating}" name="rating" value="{rating}" on:change={onChange}>
      <label for="num{rating}">{rating}</label>
    {/each}
</div>
<p>&nbsp;</p>

<style>
.radio-toolbar {
  margin: 10px;
  text-align: center;
}

.radio-toolbar input[type="radio"] {
  opacity: 0;
  position: fixed;
  width: 0;
}

.radio-toolbar label {
    display: inline-block;
    background-color: #ddd;
    width: 20px;
    height: 20px;
    padding:10px;
    font-family: sans-serif, Arial;
    font-size: 20px;
    border: 2px solid #fff;
    border-radius: 50%;
    text-align: center;
    margin: 5px
}

.radio-toolbar label:hover {
  background-color: #dfd;
}

.radio-toolbar input[type="radio"]:focus + label {
    border: 2px solid #444;
}

.radio-toolbar input[type="radio"]:checked + label {
    background-color: #1E1D37;
    color: #fff;
    font-size: 20px;
}
</style>
```
![](/assets/img4.png)
## add in and out transitions to feedback items
- FeedbackList
```javascript
<script>
	import FeedbackItem from './FeedbackItem.svelte'
  import {fade, scale} from 'svelte/transition'

  export let feedback = []
  console.log(feedback)

  // reactive value
  $: count = feedback.length 
  $: avg = feedback.length ? feedback.reduce((prev, cur) => { return {rating: prev.rating+cur.rating}}) : {}

</script>

<main>

  {#if count }
  <div class="space-around" style="font-weight:bold">
    <div class="float-left">
      <span class="badge">{count} {count == 1 ? 'review' : 'reviews'}</span>
    </div>
    <div class="float-right">
      <span class="badge">Rating Everage: {avg.rating / count}/10</span>
    </div>
  </div>
  {/if}

  {#each feedback as fb (fb.id)}
    <div in:scale out:scale>
      <FeedbackItem {fb}  on:delete-feedback/>
    </div>
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
```
