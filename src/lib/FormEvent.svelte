<script>
  import Api from './api/auth'
  let username = ''
  let password = ''
  let amountTicket = 0
  let price = 0

  export const postLogin = async () => {
    // loader = true

    try {
      const response = await Api.post('login',  {
        username: username,
        password: password,
      })
      console.log(response)
      return response
    } catch (error) {
      console.error(error)
    }
  }
</script>

<style>
  input {
    border-radius: 3px;
    font-size: 1.5rem;
    margin: 5px;
  }
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
</style>

<div class="card">

  <h1>
    SalesMan
    <span style="color: goldenrod;">Farma</span>
  </h1>
  <input bind:value={username} type="text" placeholder="Name" />
  <br />
  <input bind:value={password} type="password" placeholder="Password" />
  <br />

  <div>
    <button on:click={postLogin}>Login</button>
  </div>
</div>
