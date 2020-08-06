<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let name;
  export let points;
  let showControls = false;
  let edit = false;

  //Anonymous kind of functions
  const addPoint = () => (points += 1);
  const removePoint = () => (points -= 1);
  const toggleControls = () => (showControls = !showControls);
  const toggleEdit = () => (edit = !edit);
  const onDelete = () => dispatch("removeplayer", name);
</script>

<style>
  h1 {
    color: #1a0731;
  }

  h3 {
    margin-bottom: 10px;
  }
</style>

<div class="card">
  <h1>
    {name}
    <button class="btn btn-link" on:click={toggleEdit}>
      {#if edit}Close{:else}Edit{/if}
    </button>
    <button class="btn btn-danger btn-sm align-right" on:click={onDelete}>x</button>
    <button class="btn btn-sm align-right" on:click={toggleControls}>
      {#if showControls}-{:else}+{/if}
    </button>
  </h1>
  {#if edit}
    <form>
      <input type="text" bind:value={name} required/>
    </form>
  {/if}
  <h3>Points: {points}</h3>
  {#if showControls}
    <button class="btn" on:click={addPoint}>+1</button>
    <button class="btn btn-dark" on:click={removePoint}>-1</button>
    <input type="number" bind:value={points} />
  {/if}
</div>
