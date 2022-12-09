<script>
  import FormEvent from './lib/FormEvent.svelte'
  import ManagerScreen from './lib/ManagerScreen.svelte'
  import Pos from './lib/pos.svelte'
  import { afterUpdate } from 'svelte'
  import { token, rol } from './lib/stores/localsave'

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

</style>

<main>
  {#if tokenValue == null}
    <FormEvent />
  {:else if tokenValue != null && rolValue === 'Cashier'}
    <Pos />
  {:else if tokenValue != null && rolValue === 'Manager'}
    <ManagerScreen />
  {/if}
</main>
