<script>
  import Canvg from "canvg";
  import html2canvas from "html2canvas";
  import Content from "./Content.svelte";
  import Controls from "./Controls.svelte";

  let showDownload = false;
  let v = null;

  function handleCapture() {
    showDownload = true;
    html2canvas(document.querySelector("#capture")).then(canvas => {
      const ctx = canvas.getContext("2d");

      var s = new XMLSerializer();
      var svg = document.querySelector("svg");
      var str = s.serializeToString(svg);

      v = Canvg.fromString(ctx, str);

      v.start();

      const downloadLink = document.querySelector(".download-link");

      downloadLink.href = canvas.toDataURL();
      downloadLink.download = "myCharacter.png";
      downloadLink.innerHTML = "download me plz";
      document.body.appendChild(canvas);
    });
  }
</script>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :global(:root) {
    --color-background: white;
    --color-dark-accent: black;
    --color-primary-accent: red;
  }

  main {
    height: 100vh;
    width: 100%;
    display: grid;
    place-items: center;
  }

  #capture {
    height: 60vh;
    width: 600px;
  }
</style>

<main>
  <Controls {handleCapture} {showDownload}/>
  
  <section id="capture">
    <Content/>
  </section>
</main>