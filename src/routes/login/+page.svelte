<script>
  let email = '';
  let password = '';
  
  function handleLogin(event) {
    event.preventDefault(); 
    const formData = { email, password };
    console.log('Login submitted!', formData);
  }
</script>

<style>
    
  

  h1 {
    color: #0066cc;
    text-align: center;
  }

  form {
    max-width: 400px;
    margin: 0 auto;
    background-color: #fff;
    padding: 20px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
  }

  label {
    margin-bottom: 5px;
    color: #666;
    display: block;
  }

  input {
    padding: 8px;
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
    width: calc(100% - 16px);
  }

  button {
    padding: 10px 20px;
    background-color: #0066cc;
    color: #fff;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    width: 100%;
  }

  button:hover {
    background-color: #0052a3;
  }
</style>

<h1>Login Form</h1>
<form on:submit={handleLogin}>
  <label for="email">Email:</label>
  <input id="email" bind:value={email} type="email" required />
  
  <label for="password">Password:</label>
  <input id="password" bind:value={password} type="password" required />
  
  <button type="submit">Login</button>
</form>

  <a href="/register">Har du inget konto? Registrera</a>