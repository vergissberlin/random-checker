# Random Number Checker

A self-contained single-page app for comparing and visualising pseudo-random number generation (PRNG) algorithms. No build step, no dependencies — just open `index.html`.

**Live demo:** https://claude.ai/code/artifact/26ad0810-796e-429c-a40a-77b5aa3bfb54

---

## Features

- **5 PRNG algorithms** selectable at runtime
- Frequency histogram (SVG, 20 buckets, interactive tooltips)
- **Chi-square uniformity test** (α = 0.05, df = 100) — PASS/FAIL verdict per run
- Statistics panel: min, max, mean, median, standard deviation
- Configurable seed and sample count (100 – 10,000)
- CSV export of raw numbers
- Light / dark theme toggle

---

## Algorithms

| Algorithm | Period | Notes |
|---|---|---|
| `Math.random()` | impl-defined | Browser-native (V8: xorshift128+). Seed not possible. |
| LCG | 2³² | Linear Congruential Generator — Numerical Recipes constants. Fast, shows Marsaglia hyperplane weakness at high counts. |
| Xorshift32 | 2³² − 1 | Marsaglia (2003). XOR + shifts only. Passes most statistical tests. |
| Mersenne Twister (MT19937) | 2¹⁹⁹³⁷ − 1 | Matsumoto & Nishimura (1998). Passes Diehard tests. Default PRNG in Python and Ruby. |
| Middle-Square | short | John von Neumann (1946). Degenerates quickly — expect chi-square FAIL and visible clustering. |

---

## Usage

```bash
# No install needed — open directly in a browser
open index.html

# Or serve locally
npx serve .
python3 -m http.server
```

---

## Interpreting Results

**Chi-square test:** Checks whether the generated integers (0–100) are uniformly distributed. A value below 124.34 (critical value at α = 0.05, df = 100) means the distribution is statistically indistinguishable from uniform.

**Orange bars** in the histogram indicate buckets with more than twice the expected frequency — a visual hint at non-uniformity.

**Middle-Square** is intentionally weak. With many seeds it converges to zero within a few hundred iterations, producing a degenerate distribution.

---

## Project Structure

```
random-checker/
└── index.html   # Entire application — HTML, CSS, JS in one file
```

---

## License

MIT
