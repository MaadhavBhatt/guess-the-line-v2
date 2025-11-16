<script setup lang="ts">
import { onMounted } from 'vue';

const targetGraph = 'f(x)=x^2 + \\cos(x)';

declare global {
  interface Window {
    // eslint-disable-next-line @typescript-eslint/no-explicit-any
    Desmos: any;
  }
}

onMounted(() => {
  const elt = document.getElementById('calculator');
  if (elt && window.Desmos) {
    const calculator = window.Desmos.GraphingCalculator(elt);
    calculator.setExpression({ id: 'graph1', latex: targetGraph, secret: true });
  }
});
</script>

<template>
  <main>
    <section class="container">
      <h1>Guess The Line v2</h1>
      <p>Built by <a href="https://github.com/MaadhavBhatt">Maadhav</a></p>
    </section>

    <section class="container">
      <!-- DO NOT TOUCH
       This calculator has inline styles because applying styles from the component styles was not working as expected. -->
      <div id="calculator"
        style="width: 100%; max-width: 100rem; height: 40rem; margin: 0 auto; border: 2px solid var(--clr-black-2); border-radius: 8px;">
      </div>
    </section>
  </main>
</template>

<style>
/* Font imports */
@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');


:root {
  --font-primary: 'Inter', system-ui, -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif,
    'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';

  --clr-black-1: #121212;
  --clr-black-2: #333;
  --clr-white-1: #eee;

  --clr-text: var(--clr-black-2);
  --clr-bg: var(--clr-white-1);
}

/* Do not use !important inside layers */
@layer reset, base;

/* CSS Reset from https://www.joshwcomeau.com/css/custom-css-reset/ */
@layer reset {

  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }

  * {
    margin: 0;
    padding: 0;
  }

  @media (prefers-reduced-motion: no-preference) {
    html {
      interpolate-size: allow-keywords;
    }
  }

  body {
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
  }

  img,
  picture,
  video,
  canvas,
  svg {
    display: block;
    max-width: 100%;
  }

  input,
  button,
  textarea,
  select {
    font: inherit;
  }

  p,
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    overflow-wrap: break-word;
  }

  p {
    text-wrap: pretty;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    text-wrap: balance;
  }

  #root,
  #__next {
    isolation: isolate;
  }

  :root {
    font-size: 10px;
  }
}

@layer base {
  body {
    font-family: var(--font-primary);
    font-optical-sizing: auto;

    color: var(--clr-text);
    background-color: var(--clr-bg);

    min-height: 100vh;
  }

  .container {
    max-width: 1200px;
    width: 80%;
    margin: 0 auto;
    padding: 2rem;
    text-align: center;
  }

  a {
    text-decoration: underline;
    color: inherit;

    &:hover,
    &:focus {
      color: blue;
    }
  }

  p {
    font-size: 2rem;
  }

  h1 {
    font-size: 6rem;
  }
}
</style>
