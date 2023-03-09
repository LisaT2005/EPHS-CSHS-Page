<!--- this is from the CSHS 2022 Replit group  -->
<script>
  import { fade, fly, slide } from 'svelte/transition';
  import { quintOut } from 'svelte/easing';
  import Gallery from './ImgGallery.svelte'

  function menuSlideIn() {
    return {
      duration: 750,
      easing: quintOut,
      css: (t, u) => `transform: translateX(${u * -100}%);`
    }
  }

  function menuSlideOut() {
    return {
      duration: 500,
      easing: quintOut,
      css: (t, u) => `transform: translateX(${u * -100}%);`
    }
  }

  function animateFlip() {
    return {
      duration: 500,
      css: (t, u) => `transform: rotateX(${u * -50}%);`
    }
  }

  let menuToggled = false;
  let size = "xl";

  function toggleMenu() {
    menuToggled = !menuToggled;
  }

  function closeSidebar() {
    menuToggled = false;
  }

  const pageNames = [
    {
      name: "Home"
    },
    {
      name: "What We Do"
    },
    {
      name: "Who We Are"
    },
    {
      name: "Contact"
    }
  ];
  let pageSelectedArr = [true, false, false];

  function selectPage(index) {
    for (let i = 0; i < pageSelectedArr.length; i++) {
      pageSelectedArr[i] = false;
    }
    pageSelectedArr[index] = true;
  }

  function openSchoology() {
    window.open('https://edenpr.schoology.com/group/5300557475', '_blank');
  }

  const homeImages = [
    {
      caption: "",
      url: 'src/assets/cshsgroupphoto1.png'
    },
    {
      caption: "",
      url: 'src/assets/cshsgroupphoto2.png'
    },
    {
      caption: "",
      url: 'src/assets/csintheschools3.png'
    }
  ];

  const outreachImages = [
    {
      caption: "Co-President Lucas Wagner assisting a student",
      url: 'src/assets/csintheschools2.png'
    },
    {
      caption: "A group of students showing off their binary bracelets",
      url: 'src/assets/csintheschools1.png'
    },
    {
      caption: "Some of the committee members giving a presentation",
      url: 'src/assets/csintheschools3.png'
    }
  ];
  
</script>

<main>
  <div id=container>
    <header id=header>
      <i class="fa-solid fa-bars fa-{size}" class:rotateMe={menuToggled} id=menutoggle on:mousedown={toggleMenu}></i>
      <h1 id=titletext>
        <span class="desktop-title">EDEN PRAIRIE CSHS</span>
        <span class="mobile-title">EP CSHS</span>
      </h1>
<!--       <i class="fa-solid fa-house fa-{size}" id=homebutton on:mousedown={() => selectPage(0)}></i> -->
      <img src="src/assets/schoologylogo.svg" title="CSHS Schoology Group" id=schoologybutton on:mousedown={openSchoology}>
    </header>
    <div id=body>
      {#if menuToggled}
        <div id=sidebar in:menuSlideIn out:menuSlideOut>
          {#each pageNames as page, i}
            <button class=menubuttons class:pageSelected={pageSelectedArr[i]} on:click={() => selectPage(i)}>{page.name}</button>
          {/each}
        </div>
      {/if}
      {#if pageSelectedArr[0]}
        <div class=bodycontent id=homecontent on:mousedown={closeSidebar}>
          <h1 class=pagetitle>HOME</h1>
          <p>EPHS Computer Science Honor Society is a part of the National Computer Science Honor society. It recognizes young students who have demonstrated interest, passion, and academic excellence in the subjects of computer science. Computer Science Honors Society is about working together to solve problems, help others, or create cool things! Head over to the "What We Do" page to learn about what you can participate in.</p>
          <Gallery images={homeImages}/>
          <h1 class=subtitle>HOW TO JOIN</h1>
          <p>To join the Computer Science Honors Society you must have completed at least one term of a Computer Science course in good standing.</p>
        </div>
      {/if}
      {#if pageSelectedArr[1]}
        <div class=bodycontent id=whatwedocontent on:mousedown={closeSidebar}>
          <h1 class=pagetitle>WHAT WE DO</h1>
          <p>The Computer Science Honors Society has a few main committees. Committees participate in events, create projects, and more. Currently our main committees are the Outreach Committee, Website Committee, and Java Help Committee. You can choose which one(s) to be apart of based on your own interest!</p>
          <h1 class=subtitle>Outreach Committee</h1>
          <p>The Outreach Committee's goal is to get more people interested in Computer Science. Computer Science is only becoming more important in the world. We believe that it is crucial for people to have a basic understanding, if not more, of computers and how they work. This year, the committee spent time in multiple Eden Praire elementary schools teaching 5th graders Computer Science basics. Things like binary and encryption, to hopefully spark an interest in such an important field.</p>
          <Gallery images={outreachImages}/>
          <h1 class=subtitle>Website Committee</h1>
          <p>The Website Committee is a team of members who develop websites such as this one. This website was designed and developed from scratch using code, not a website builder. We also work on websites for other clubs who need one. For those interested in learning or developing their programming skills this is a great way to do so! Or you can help without coding, if your interest is designing and planning.</p>
        </div>
      {/if}
      {#if pageSelectedArr[2]}
        <div class=bodycontent id=whowearecontent on:mousedown={closeSidebar}>
          <p>This is the who we are page.</p>
        </div>
      {/if}
    </div>
    <footer id="footer">
      <h1 id="footertext"></h1>
    </footer>
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
/*   html, main {
    padding: 0;
    margin: 0;
  } */

  main {
    padding: 0;
    margin: 0;
    font-size: 20px;
    box-sizing: border-box;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

/*   header {
/*     background-color: #ff3e00; */
/*     background-color: #d9d9d9; */
/*     background-color: #1C2541; */
/*     background-color: #0B132B; */
/*     background-color: #1a1c24;
  } */

  #header {
    background-color: #1a1c24;
    grid-area: header;
    width: 100%;
    display: flex;
    justify-content: left;
    align-items: center;
    height: 4rem;
  }

  #footer {
    background-color: #4fb2d4;
/*     background-color: #1a1c24; */
/*     height: 10vh; */
    height: 8rem;
    display: flex;
    margin-top: 10%;
  }

  #footertext {
    font-size: 2rem;
    align-self: center;
    margin: 0 auto;
  }

  #menutoggle {
    background-color: rgba(0, 0, 0, 0);
    margin: 0 2%;
    transition: all 0.45s ease;
    color: white;
  }

  #titletext {
    font-size: 3rem;
/*     color: #4FB2D4; */
    overflow: hidden; 
    white-space: nowrap;
  }
  
  .desktop-title {
    display: block;
  }

  .mobile-title {
    display: none;
  }

  #sidebar {
    background-color: rgb(40, 40, 40);
/*     background-color: #0B132B; */
    grid-area: sidebar;
    position: relative;
    z-index: 1;
    min-width: 20%;
    max-width: 20%;
    min-height: 100%;
    flex-grow: 1;
    top: 0;
    left: 0;
    transition: 0.2 ease-in-out;
  }

  #body {
    grid-area: body;
/*     background-color: darkred; */
    position: relative;
    display: flex;
    overflow: none;
    flex-grow: 1;
    min-height: 100vh;
  }

  .bodycontent {
    flex-grow: 1;
  }

  .menubuttons {
    width: 100%;
    background-color: rgb(40, 40, 40);
    font-weight: 300;
    color: white;
    line-height: 1;
    text-transform: uppercase;
    padding: 3% 0;
    border: none;
    font-size: 1.5rem;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  .menubuttons:hover {
    background-color: rgb(50, 50, 50);
  }

  .pageSelected {
    background-color: rgb(50, 50, 50);
    border-left: 10px solid #4fb2d4;
  }

  #schoologybutton {
    margin-left: auto;
    margin-right: 2%;
    color: white;
    height: 2.5rem;
    width: 2.5rem;
/*     font-weight: 400;
    padding: 0 2%;
    min-height: 100%;
    color: black;
    line-height: 1;
    text-transform: uppercase;
    border: none;
    font-size: 1.5rem;
    background-color: #d9d9d9;
    font-family: Roobert,-apple-system,BlinkMacSystemFont,"Segoe UI",Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol"; */
  }

  #homebutton:hover {
    background-color: #f1f1f1;
  }

  .pagetitle {
    color: black;
    margin: 2% auto;
    font-weight: 300;
    font-size: 4.5rem;
  }

  .subtitle {
    color: black;
    margin: 5% auto 2% auto;
    font-weight: 300;
    font-size: 3.5rem;
  }
  
  h1 {
    color: white;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1;
    text-align: center;
  }

  p {
    margin: 1rem auto;
    line-height: 1.35;
    text-align: center;
    max-width: 75%;
    font-size: 1.4rem;
  }

  #container {
    width: 100%;
    height: fit-content;
    display: flex;
    flex-direction: column;
/*     display: grid;
    grid-template-columns: minmax(0, 1fr);
    grid-template-rows: minmax(3.5rem, 0.07fr) minmax(0, 1fr);
    grid-template-areas:
      "header"
      "body"; */
  }

  .rotateMe {
    transition: all 0.25s ease;
    transform: rotate(-90deg);
  }

  @media screen and (max-width: 480px) {
    #titletext {
/*       font-size: 2rem; */
    }

    #homebutton {
      margin-right: 3%;
    }

    #menutoggle {
      margin: 0 3%;
    }

    #sidebar {
      min-width: 100%;
      position: absolute;
    }
    
    .menubuttons {
      font-size: 1.5rem;
    }

    .desktop-title {
      display: none;
    }

    .mobile-title {
      display: block;
    }
    
    h1 {
      max-width: none;
    }

    p {
      max-width: 90%;
      font-size: 1.25rem;
    }
  }
</style>
