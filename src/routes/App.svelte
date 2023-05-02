<script>
  let prompt = "";
  let generatedText = "";
  let error = "";

  function handleSubmit(event) {
    event.preventDefault();

    fetch(`http://localhost:8000/generate?prompt=${encodeURIComponent(prompt)}`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    })
      .then((response) => response.json())
      .then((data) => {
        generatedText = data.generated_text;
        error = "";
      })
      .catch((err) => {
        generatedText = "";
        error = err.message;
      });
  }
</script>

<main>
  <form on:submit={handleSubmit}>
    <label>
      Prompt:
      <input type="text" bind:value={prompt} />
    </label>
    <button type="submit">Generate</button>
  </form>

  {#if generatedText}
  <textarea>{generatedText}</textarea>
  {:else if error}
  <p>{error}</p>
  {/if}
</main>

<style>
  textarea {
    width: 100%;
    height: 200px;
  }
</style>
