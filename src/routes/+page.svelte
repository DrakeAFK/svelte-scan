<script>
  import QRCode from 'qrcode'
  import { onMount } from 'svelte'

  let qrCodeUrl = ''

  // With async/await
  const generateQR = async text => {
    try {
      qrCodeUrl = await QRCode.toDataURL(text)
    } catch (err) {
      console.error(err)
    }
  }

  onMount(() => {
    // Initial QR code generation example
    generateQR('https://youtu.be/dQw4w9WgXcQ?si=52Vp0I_gQY3aeXYp')
  })

  const saveQRCode = () => {
    const link = document.createElement('a')
    link.href = qrCodeUrl
    link.download = 'generated_qr_code.png'
    link.click()
  }
</script>

<h1 class="text-center text-5xl text-primary p-10">Svelte Scan</h1>

<div class="border rounded-lg mx-auto text-center py-10 min-w-[250px] w-1/2">
  <h2 class="text-center text-2xl">Generate a QR Code</h2>
  <p class="text-center italic pt-3 pb-5">Insert a link or any other text</p>

  <div class="space-y-5">
    <input
      class="rounded-md p-2"
      type="text"
      placeholder="https://drakeafk.io"
      on:input={e => generateQR(e.target.value)}
    />
  
    {#if qrCodeUrl}
      <img class="mx-auto rounded-lg" src={qrCodeUrl} alt="Generated QR Code" />
      <button class="btn btn-accent" on:click={saveQRCode}>Save QR Code</button>
    {/if}
  </div>
</div>

<div class="py-5 mx-auto max-w-fit">
  <footer class="footer footer-center p-3 rounded-md bg-base-300 text-base-content">
    <aside>
      <p>Developed by <a class="link-accent" href="https://drakeafk.io" target="_blank">DrakeAFK</p>
      <p>View Svelte Scan on <a class="link-primary" href="https://github.com/DrakeAFK/svelte-scan" target="_blank">GitHub</a></p>
    </aside>
  </footer>
</div>