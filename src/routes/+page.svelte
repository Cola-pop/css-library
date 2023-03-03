<script>
  import { onMount } from 'svelte';

  let cursor = null;
  let links = [];
  let initCursor = false;

  onMount(() => {
    cursor = document.querySelector('.custom-cursor');
    links = document.querySelectorAll('button');
    initCursor = false;

    for (let i = 0; i < links.length; i++) {
      let selfLink = links[i];

      selfLink.addEventListener('mouseover', function () {
        cursor.classList.add('custom-cursor--link');
      });
      selfLink.addEventListener('mouseout', function () {
        cursor.classList.remove('custom-cursor--link');
      });
    }
  });

  const handleMouseMove = (e) => {
    let mouseX = e.clientX;
    let mouseY = e.clientY;

    if (!initCursor) {
      // cursor.style.opacity = 1;
      TweenLite.to(cursor, 0.3, {
        opacity: 1,
      });
      initCursor = true;
    }

    TweenLite.to(cursor, 0, {
      top: mouseY + 'px',
      left: mouseX + 'px',
    });

    e.preventDefault();
  };

  const handleMouseOut = (e) => {
    TweenLite.to(cursor, 0.3, {
      opacity: 0,
    });
    initCursor = false;
  };
</script>

<svelte:window on:mousemove={handleMouseMove} on:mouseout={handleMouseOut} />

<svelte:head>
  <title>CSS Library</title>
  <meta name="description" content="Svelte CSS demo app" />
  <script
    src="http://cdnjs.cloudflare.com/ajax/libs/gsap/1.18.0/TweenMax.min.js"
  ></script>
</svelte:head>

<body>
  <div class="container">
    <div class="row">
      <div class="column">
        <button
          class="btn-outlined animate bounce animate--slow animate--infinite"
        >
          Bouncing Button
        </button>
      </div>
      <div class="column">
        <button
          class="btn-outlined animate daffy animate--slow animate--infinite"
        >
          Daffy Button
        </button>
      </div>
    </div>
    <div class="row">
      <div class="column">
        <button class="btn">Button</button>
      </div>
    </div>
    <div class="row">
      <div class="column">
        <h1 class="animate slideInLeft animate--fast">Hello, World!</h1>
      </div>
      <div class="column">
        <h5 class="animate rotate animate--slow animate--infinite">hahayy</h5>
      </div>
    </div>
    <div class="row">
      <div class="column">
        <h3
          class="animate slideInLeft animate--slow animate--infinite animate--alternate"
        >
          can't catch me
        </h3>
      </div>
    </div>
  </div>
  <div class="custom-cursor" />
</body>

<style>
</style>
