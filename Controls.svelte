<script>
export let handleCapture;
export let showDownload;
import { fillColor, lettersColor, lettersOutline } from "./store.js";
</script>

<style>
	.controls {
	  position: fixed;
	  top: 0;
	  left: 0;
	  width: 100%;
	}
</style>

<div class="controls">
	<label name="fill color">Fill Color</label>
	<input type="color" for="fill color" on:change={e => fillColor.set(e.target.value)} bind:value={$fillColor}>
	<label>Letters Color</label>
	<input name="letters color" type="color" on:change={e => lettersColor.set(e.target.value)} bind:value={$lettersColor} />
	<label name="letters outline">Letters Outline</label>
	<input name="letters outline" type="color" on:change={e => lettersOutline.set(e.target.value)} bind:value={$lettersOutline} />

	  <div class="buttons-container">
    <button on:click={handleCapture}>capture</button>
		{#if showDownload}
		<a href="/" class="download-link">download image</a>
		{/if}
  </div>
</div>