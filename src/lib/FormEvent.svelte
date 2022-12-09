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

<style>

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
