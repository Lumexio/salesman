<script>
  import Api from './api/auth'
  import { token, rol } from './stores/localsave'
  import { openModal } from 'svelte-modals'
  import Modal from './ModalProduct.svelte'

  function handleClick() {
    openModal(Modal, { title: 'Alert', message: 'This is an alert' })
  }

  let arrayProducts = []
  let productid = null
  let itemsTitle = [{ title: 'id' }, { title: 'Nombre' }, { title: 'Precio' }]
  const getProduct = async () => {
    // loader = true
    try {
      const response = await Api.get('product/list')
      arrayProducts = response
      return response
    } catch (error) {
      console.error(error)
    }
  }
  const deleteProduct = async () => {
    // loader = true
    try {
      const response = await Api.delet('product/delete/', productid)
      return response
    } catch (error) {
      console.error(error)
    }
  }

  getProduct()
</script>

<style scoped>
  .containerSale {
    display: grid;
    width: 100%;
    place-items: center center;
    grid-auto-rows: 18em;
    grid-auto-flow: dense;
    gap: 1em;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 300px), 1fr));
  }
  .tableContainer {
    width: 100%;
    grid-column: 1/3;
    text-align: center;
  }
  table,
  th,
  td {
    border-bottom: 1px solid;
  }
</style>

<div class="card">
  <button on:click={handleClick}>Crear Producto</button>
  <table class="tableContainer">
    <thead>
      <tr>
        {#each itemsTitle as item}
          <th>{item.title}</th>
        {/each}
      </tr>
    </thead>
    <tbody>
      {#each arrayProducts as item}
        <tr>
          <td>{item.id}</td>
          <td>{item.name}</td>
          <td>{item.price}mxn</td>
        </tr>
      {/each}
    </tbody>
  </table>
  <input bind:value={productid} type="number" placeholder="Product id" />
  <button on:click={deleteProduct}>Delete</button>
</div>
