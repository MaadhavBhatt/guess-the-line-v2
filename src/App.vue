<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { graphs } from './data/graphs';
import HelpModal from './components/HelpModal.vue';

const showHelp = ref(true);

let targetGraph: string = graphs[0] || 'f(x)=x';

declare global {
  interface Window {
    // eslint-disable-next-line @typescript-eslint/no-explicit-any
    Desmos: any;
  }
}

onMounted(() => {
  const elt = document.getElementById('calculator');
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  let calculator: any = null;

  if (elt && window.Desmos) {
    calculator = window.Desmos.GraphingCalculator(elt);
    calculator.setExpression({
      id: 'targetGraph',
      latex: targetGraph,
      secret: true,
    });
  }

  document.getElementById('newGraph')?.addEventListener('click', () => {
    targetGraph = graphs[Math.floor(Math.random() * graphs.length)] || 'f(x)=x';
    if (calculator) {
      calculator.setExpression({
        id: 'targetGraph',
        latex: targetGraph,
        secret: true,
      });
    } else if (elt && window.Desmos) {
      // fallback: initialize calculator if it wasn't ready earlier
      calculator = window.Desmos.GraphingCalculator(elt);
      calculator.setExpression({
        id: 'targetGraph',
        latex: targetGraph,
        secret: true,
      });
    } else {
      // Desmos not available yet
      console.warn('Desmos not available to update the graph.');
    }
  });
});
</script>

<template>
  <main>
    <header>
      <h1>
        functionGuesser
        <span class="subscript uppercase">/ Guess The Line v2</span>
      </h1>
      <p>
        Built with &#10084; by
        <a target="_blank" href="https://github.com/MaadhavBhatt">Maadhav</a>
      </p>
    </header>
    <HelpModal :isOpen="showHelp" @close="showHelp = false" />
    <section>
      <!-- DO NOT TOUCH
       This calculator has inline styles because applying styles from the component styles was not working as expected.
       The height is set as 100vh minus the height of the header -->
      <div
        id="calculator"
        style="width: 100%; height: calc(100vh - 65.25px); margin: 0 auto"
      ></div>
      <div class="buttons">
        <button type="button" class="new-btn" id="newGraph">New graph</button>
        <button type="button" class="help-btn" @click="showHelp = true">
        ?
      </button>
      </div>
    </section>
  </main>
</template>

<style>
/* Font imports */
@import url('https://fonts.googleapis.com/css2?family=Stack+Sans+Notch:wght@200..700&display=swap');

:root {
  --font-primary:
    'Stack Sans Notch', system-ui, -apple-system, BlinkMacSystemFont,
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

  h2 {
    font-size: clamp(1.8rem, 4vw, 2.4rem);
  }

  code {
    background-color: rgba(0, 0, 0, 0.1);
    padding-inline: 0.4rem;
    border-radius: 0.3rem;
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

  .buttons {
    position: absolute;
    inset: auto 1rem 1rem auto;
    display: flex;
    flex-direction: row-reverse;
    justify-content: center;
    align-items: center;
    gap: 1.5rem;

    & > button {
      font-size: clamp(1.5rem, 1.5vw, 2rem);
    color: var(--clr-bg);
    background-color: var(--clr-text);

    &:hover,
    &:focus {
      color: var(--clr-text);
      outline: 2px solid var(--clr-text);
        background-color: var(--clr-bg);
    }
  }

    & > .new-btn {
    padding: 0.5em 1em;

    border-radius: 1rem;
    cursor: pointer;
  }

    & > .help-btn {
      width: 2em;
    aspect-ratio: 1 / 1;

    border-radius: 50%;
    cursor: pointer;
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
