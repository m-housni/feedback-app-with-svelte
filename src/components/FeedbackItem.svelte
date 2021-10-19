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
    font-size: 20px;
  }

  .close {
    position: absolute;
    top: 10px;
    right:20px;
    cursor: pointer;
  }
</style>
