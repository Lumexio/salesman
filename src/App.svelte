<script>
  import FormEvent from './lib/FormEvent.svelte'
  import ManagerScreen from './lib/ManagerScreen.svelte'
  import Pos from './lib/pos.svelte'
  import { afterUpdate } from 'svelte'
  import { token, rol } from './lib/stores/localsave'
  import { Modals, closeModal } from 'svelte-modals'

  let tokenValue
  let rolValue
  token.subscribe((value) => {
    tokenValue = value
  })
  rol.subscribe((value) => {
    rolValue = value
  })
  afterUpdate(() => {})
</script>

<style>
  .backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
  }
</style>

<main>
  {#if tokenValue == null}
    <FormEvent />
  {:else if tokenValue != null && rolValue === 'Cashier'}
    <Pos />
  {:else if tokenValue != null && rolValue === 'Manager'}
    <ManagerScreen />
    <Modals>
      <div slot="backdrop" class="backdrop" on:click={closeModal} />
    </Modals>
  {/if}
</main>
