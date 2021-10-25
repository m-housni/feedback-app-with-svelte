<script>
  import {createEventDispatcher} from 'svelte' // allows event dispatching
  const dispatch = createEventDispatcher() // allows to call dispatch('event-name',value)
  let ratings =  [1,2,3,4,5,6,7,8,9,10] // rating values

  const onChange = (e) => {
    // arrow function (introduced in ES6) to dispatch event on rating select
    dispatch('rating-select', e.currentTarget.value)
  }
</script>

<div class="radio-toolbar">
    <!-- loop to generate: (1), (2) ... -->
    {#each ratings as rating (rating)}
      <input type="radio" id="num{rating}" name="rating" value="{rating}" on:change={onChange}>
      <label for="num{rating}">{rating}</label>
    {/each}
</div>

<style>
  .radio-toolbar {
    margin: 10px;
    text-align: center;
  }

  .radio-toolbar input[type="radio"] {
    /* hide the default radio button */
    opacity: 0;
    position: fixed;
    width: 0;
  }

  .radio-toolbar label {
    /* style the label to look like a round button */
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
    /* change a bit the label color on hover */
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