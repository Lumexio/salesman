<script>
  import Api from './api/auth'
  import { token, rol } from './stores/localsave'
  let username = ''
  let password = ''
  let amountTicket = 0
  let price = 0

  export const postLogin = async () => {
    // loader = true
    try {
      const response = await Api.post('login', {
        username: username,
        password: password,
      })
      token.set(response.token)
      rol.set(response.position)
      return response
    } catch (error) {
      console.error(error)
    }
  }
</script>

<style scoped>
  button {
    background-color: black;
    border: transparent;
    font-size: 1.2rem;
  }
  button:hover {
    background-color: goldenrod;
    color: black;
    border: transparent;
  }
  .h-full {
    height: 40rem;
    width: 20rem;
  }
  #saletext {
    --tw-text-opacity: 1;
    color: rgba(255, 255, 255, var(--tw-text-opacity));
  }
  .fullwithbutton {
    width: 100%;
    height: 4rem;
    padding: 0;
  }
  .cartSpace {
    height: 80%;
  }
</style>

<div class="card h-full">
  <div cartSpace>
    <p>sadasd</p>
  </div>
  <div>
    <button class="fullwithbutton" on:click={postLogin}>
      <p id="saletext">Submit</p>
    </button>
  </div>
</div>
