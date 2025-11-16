<script setup lang="ts">
import { onMounted } from 'vue';

const targetGraph: string = 'f(x)=x^{1.5} - 2x + \\sin(x)';

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
    calculator.setExpression({ id: 'targetGraph', latex: targetGraph, secret: true });
  }
});
</script>

<template>
  <main>
    <header>
      <h1>functionGuesser <span class="subscript uppercase">/ Guess The Line v2</span></h1>
      <p>Built with &#10084; by <a target="_blank" href="https://github.com/MaadhavBhatt">Maadhav</a></p>
    </header>
    <section>
      <!-- DO NOT TOUCH
       This calculator has inline styles because applying styles from the component styles was not working as expected.
       The height is set as 100vh minus the height of the header -->
      <div id="calculator" style="width: 100%; height: calc(100vh - 65.25px); margin: 0 auto;">
      </div>
      <button type="button" class="new-btn" id="newGraph">New graph</button>
    </section>
  </main>
</template>

<style>
/* Font imports */
@import url('https://fonts.googleapis.com/css2?family=Stack+Sans+Notch:wght@200..700&display=swap');

:root {
  --font-primary: 'Stack Sans Notch', system-ui, -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif,
    'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';

  --clr-black-1: #121212;
  --clr-black-2: #333;
  --clr-white-1: #fff;
  --clr-white-2: #eee;

  --clr-text: var(--clr-black-1);
  --clr-bg: var(--clr-white-2);
}

::selection {
  background-color: var(--clr-text);
  color: var(--clr-bg);
}

/* Do not use !important inside layers */
@layer reset, base, components, utilities;

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
  }

  a {
    text-decoration: underline;
    color: var(--clr-bg);
    background-color: var(--clr-text);

    &:hover,
    &:focus {
      color: var(--clr-text);
      background-color: var(--clr-bg);
    }
  }

  p {
    font-size: clamp(1.2rem, 2vw, 2rem);
  }

  h1 {
    font-size: clamp(2rem, 5vw, 3rem);
  }
}

@layer components {
  main {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: stretch;
  }

  header {
    background-color: var(--clr-bg);
    padding: 1rem 2rem;

    text-align: center;
    letter-spacing: 1.2px;

    display: flex;
    flex-direction: column;
    gap: 1rem;

    @media screen and (min-width: 800px) {
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
    }
  }

  .new-btn {
    position: absolute;
    inset: auto 1rem 1rem auto;
    padding: 0.5em 1em;

    font-size: clamp(1rem, 1.5vw, 2rem);
    color: var(--clr-bg);

    background-color: var(--clr-text);
    border-radius: 1rem;
    cursor: pointer;

    &:hover,
    &:focus {
      background-color: var(--clr-bg);
      color: var(--clr-text);
      outline: 2px solid var(--clr-text);
    }
  }
}

@layer utilities {
  .subscript {
    font-size: clamp(1rem, 1vw, 1.5rem);
    vertical-align: sub;
    color: var(--clr-text);
    opacity: 0.7;
  }

  .uppercase {
    text-transform: uppercase;
  }
}
</style>
