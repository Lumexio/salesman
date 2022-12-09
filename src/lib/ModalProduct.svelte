<script>
  import { closeModal } from 'svelte-modals'
  import Api from './api/auth'
  // provided by <Modals />
  export let isOpen

  export let name
  export let price
  export let description

  export const postProduct = async () => {
    // loader = true
    try {
      const response = await Api.post('product/register', {
        name: name,
        description: description,
        price: price,
      })

      return response
    } catch (error) {
      console.error(error)
    }
  }
</script>

<style>
  .modal {
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;

    /* allow click-through to backdrop */
    pointer-events: none;
  }

  .contents {
    min-width: 240px;
    border-radius: 6px;
    padding: 16px;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    pointer-events: auto;
  }

  .actions {
    margin-top: 32px;
    display: flex;
    justify-content: flex-end;
  }
</style>

{#if isOpen}
  <div role="dialog" class="modal">
    <div class="contents card">
      <h1>Create ticket</h1>
      <input bind:value={name} type="text" placeholder="Name" />
      <br />
      <input bind:value={description} type="text" placeholder="Description" />
      <br />
      <input bind:value={price} type="number" placeholder="Price" />

      <div class="actions">
        <button on:click={closeModal}>Close</button>
        <button on:click={postProduct}>Create</button>
      </div>
    </div>
  </div>
{/if}
