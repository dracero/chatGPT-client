<script>
    let question = '';
    let answer = '';
  
    async function handleSubmit() {
      const response = await fetch('http://localhost:8000/chat', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify([question])
      });
  
      const data = await response.json();
      answer = data.response;
    }
  </script>
  
  <main>
    <h1>Chatbot con GPT-3 y Svelte</h1>
    <form on:submit|preventDefault={handleSubmit}>
      <label>
        Ingresa tu pregunta:
        <input type="text" bind:value={question} />
      </label>
      <button type="submit">Enviar</button>
    </form>
    {#if answer}
      <p>Respuesta: {answer}</p>
    {/if}
  </main>
  