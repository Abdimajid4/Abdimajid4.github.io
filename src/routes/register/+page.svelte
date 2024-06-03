<script>
  let firstName = '';
  let lastName = '';
  let email = '';
  let password = '';
  
  function handleSubmit(event) {
    event.preventDefault(); 
    const formData = { firstName, lastName, email, password };
    console.log('Form submitted!', formData);
  }
</script>

<style>


  form {
    display: grid;
    grid-template-columns: repeat(2, minmax(200px, 1fr));
    background-color: #fff;
    padding: 20px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  }

  label {
    margin-bottom: 5px;
    color: #666;
  }

  input {
    padding: 8px;
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  button {
    padding: 10px 20px;
    background-color: #0066cc;
    color: #fff;
    border: none;
    cursor: pointer;
  }

  button:hover {
    background-color: #0052a3;
  }
</style>

<h1>Registration Form</h1>
<form on:submit={handleSubmit}>
  <label for="firstName">First Name:</label>
  <input id="firstName" bind:value={firstName} required />
  
  <label for="lastName">Last Name:</label>
  <input id="lastName" bind:value={lastName} required />
  
  <label for="email">Email:</label>
  <input id="email" bind:value={email} type="email" required />
  
  <label for="password">Password:</label>
  <input id="password" bind:value={password} type="password" required />
  
  <button type="submit">Register</button>
</form>
<a href="/login">Har du ett konto? login</a>

