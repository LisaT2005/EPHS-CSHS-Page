<script>
  export let images = [];

  let selectedImage = [true];
  for (let i = 1; i < images.length; i++) {
    selectedImage.push(false);
  }
  let selectedImageIndex = 0;
  let selectedImageCaption = images[0].caption;

  let size = "3x";

  function changeImageRight() {
    let index = selectedImageIndex;
    selectedImage[index] = false;
    if (index + 1 == selectedImage.length) {
      index = -1;
    }
    selectedImage[index + 1] = true;
    selectedImageIndex = index + 1;
    selectedImageCaption = images[index + 1].caption;
  }

  function changeImageLeft() {
    let index = selectedImageIndex;
    selectedImage[index] = false;
    if (index - 1 < 0) {
      index = selectedImage.length;
    }
    selectedImage[index - 1] = true;
    selectedImageIndex = index - 1;
    selectedImageCaption = images[index - 1].caption;
  }
</script>

<body>
  {#each images as image, i}
    {#if selectedImage[i]}
<!--       <figure>
        <img class=galleryimage src={image.url}/>
        <figcaption>Caption goes here</figcaption>
      </figure> -->
      <img class=galleryimage src={image.url}>
    {/if}
  {/each}
  {#if selectedImageCaption != ""}
    <div id=caption>
      <h1 id=captiontext>{selectedImageCaption}</h1>
    </div>
  {/if}
  <div class=changeparent id=left>
    <i class="fa-solid fa-angle-left fa-{size} changeimage" on:mousedown={() => changeImageLeft()}></i>
  </div>
  <div class=changeparent id=right>
    <i class="fa-solid fa-angle-right fa-{size} changeimage" on:mousedown={() => changeImageRight()}></i>
  </div>
</body>

<style>
  body {
    width: 50%;
    min-width: 20rem;
    min-height: 13rem;
    height: 30vw;
    margin: 2% auto;
    position: relative;
    border: 0.25rem solid black;
    font-size: 1.5vw;
  }
  
  .galleryimage {
    object-fit: cover;
    width: 100%;
    height: 100%;
  }

  #caption {
    background-color: rgba(0, 0, 0, 0.9);
    padding: 0%;
    padding: 1% 0;
    width: 100%;
/*     margin-top: -0.25rem; */
    
/*     border: 0.25rem solid black; */
    position: absolute;
    bottom: 0%;
  }

  #captiontext {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    color: white;
    font-weight: 300;
    font-size: 1.5rem;
    text-align: center;
    padding: 0;
    margin: 0;
  }

  .changeimage {
    color: rgba(255, 255, 255, 1);
  }

  .changeparent {
    width: 3.5vw;
    display: flex;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.75);
    position: absolute;
  }

  #left {
    top: 40%;
    left: 2%;
  }

  #right {
    top: 40%;
    right: 2%;
  }

  @media screen and (max-width: 480px) {
    body {
      width: 90%;
      height: 70vw;
      font-size: 4vw;
      min-width: 0;
    }

    #left {
      top: 3%;
      left: 3%;
    }

    #right {
      top: 3%;
      right: 3%;
    }

    .changeparent {
      width: 10vw;
    }

    #captiontext {
      font-size: 1.25rem;
    }
  }
</style>