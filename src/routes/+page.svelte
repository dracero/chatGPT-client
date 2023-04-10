<script>
    import App from "./App.svelte";
    let text = '';
  
    const uploadFile = async (event) => {
      event.preventDefault();
      const formData = new FormData();
      formData.append('file', event.target.files[0]);
  
      const response = await fetch('http://localhost:8000/image-to-text', {
        method: 'POST',
        body: formData,
      });
  
      const data = await response.json();
      console.log(data.text);
      text = data.text;
    };
  </script>
  
  <form>
    <input type="file" on:change={uploadFile} />
        <p>{text}</p>
        {#if !text}
        <p>Upload an image to get the text</p>
        {/if}
  </form>
  <App />
  