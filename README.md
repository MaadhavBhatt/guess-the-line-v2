# Guess The Line V2

This project builds on the "Guess The Line" concept on the [r/desmos](https://www.reddit.com/r/desmos/) subreddit, where users try to guess a hidden graph based on its equation and [webgoatguy](https://www.youtube.com/@webgoatguy)'s YouTube [video](https://youtu.be/XS9EsvZ1mWY?si=CSSyoSvHGXgMHh5U).

This project will be submitted to [Hack Club](https://hackclub.com/)'s [Midnight](https://midnight.hackclub.com/) hackathon. If you're a teen interested in coding, check out Hack Club!

## How to Suggest a New Graph?

1. Edit the `/src/data/graphs.ts` file [here](./src/data/graphs.ts).
2. Add your desired graph equation in the format `f(x)=...` on a new line.
3. Make sure to follow the existing formatting and conventions in the file. I'll write a formatting guide soon.
4. Attach a screenshot of the graph plotted on Desmos for reference.
5. Submit a pull request with your changes.

### Graph Function Format

- Use `f(x)=...` format for defining functions.
- Use '\\' for escaping `cos`, `sin`, `tan`, etc. (e.g., `\\cos(x)`).
- Ensure the function is compatible with Desmos syntax.

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
