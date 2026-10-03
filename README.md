# RC Circuits: Currents That Change with Time

This is an interactive, browser-based demo of RC circuits. It shows how a capacitor charges and discharges through a resistor, and how the time constant τ = RC sets the pace. It comes as two separate pages, one in English and one in Korean.

Created by **Claude Opus 5.5**, based on the lecture notes by **Sang Hoon Lee (이상훈)**.

> **한국어 요약:** 축전기가 저항기를 통해 충전되고 방전되는 과정과, 시간상수 τ = RC가 그 시간 스케일을 정하는 원리를 직접 조작해 볼 수 있는 인터랙티브 웹 데모입니다. 이상훈(Sang Hoon Lee)의 강의 노트를 바탕으로 Claude Opus 5.5가 만들었습니다. 한국어 페이지는 `rc-ko.html`입니다.

## Files

| File | Description |
| --- | --- |
| `rc-en.html` | American English version |
| `rc-ko.html` | Korean version (한국어) |
| `README.md` | This file |

Each page is a single self-contained HTML file with inline CSS and JavaScript. There is no build step and there are no dependencies. The only external request is to Google Fonts for IBM Plex Sans KR, and the page falls back to system fonts if that request fails. Each page links to the other language from its top bar.

## Running it

Open either file directly in a modern browser, or serve the folder locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/rc-en.html
```

### Publishing on GitHub Pages

1. Push these files to a repository.
2. In **Settings → Pages**, choose **Deploy from a branch**, then select your branch and the root folder.
3. Visit `https://<user>.github.io/<repo>/rc-en.html` or `.../rc-ko.html`.

You can keep these pages in the same repository as the companion demo on current, resistance, and DC circuits (`circuits-en.html` and `circuits-ko.html`). The file names don't collide.

## What's inside

The four sections follow the order of the lecture notes. Every value is recomputed live as you move the controls.

1. **The RC circuit:** A live circuit with a two-way switch S. Set it to **a** to charge the capacitor or **b** to discharge it. Flipping the switch at any moment starts a new exponential approach toward the new equilibrium. The simulation runs in real time, with 0.25×, 1×, and 4× playback. While it runs, current dots flow and reverse direction on discharge, charge builds up on the capacitor plates, and q(t) and i(t) are traced against the theoretical curves. A live bar shows the loop rule ℰ = iR + q/C, with the emf shared between the resistor and the capacitor.
2. **Charging:** The solution q(t) = Cℰ(1 − e<sup>−t/RC</sup>) and i(t) = (ℰ/R)e<sup>−t/RC</sup>, with markers at τ and 2τ. Pick any time t, and the values are substituted into ℰ − iR − q/C to show it equals 0 at every t.
3. **Time constant τ = RC:** A derivation that Ω·F = s, followed by a side-by-side comparison of two circuits with different R and C. A table lists the remaining and charged fractions at τ, 2τ, 3τ, and 5τ (1/e ≈ 0.37, 1/e², …).
4. **Discharging:** The solution q(t) = q₀e<sup>−t/RC</sup> and i(t) = −(q₀/RC)e<sup>−t/RC</sup>, with a substitution check of R dq/dt + q/C = 0. A short note explains why the current is negative.

## Notes on the model

- The circuit is ideal: the battery has no internal resistance, and the wires and switch have no resistance. R ranges over 10–200 kΩ and C over 5–100 μF, so τ runs from 50 ms to 20 s and can be watched in real time.
- Every frame, the simulation updates the charge with the exact exponential step q ← q<sub>∞</sub> + (q − q<sub>∞</sub>)e<sup>−Δt/τ</sup>, so it stays accurate at any frame rate.
- Changing ℰ, R, or C during a run keeps the capacitor's present charge and restarts the time axis from that moment.
- The pages follow the system light or dark setting and respect `prefers-reduced-motion`, which starts the simulation paused.

## Credits

- Lecture notes: Sang Hoon Lee (이상훈)
- Demo design and code: Claude Opus 5.5

## License

No license has been chosen yet. Before publishing, add a `LICENSE` file if you want others to reuse the code. Also confirm with the author of the lecture notes how their material may be shared.
