# bmwdash

A live dashboard for a **BMW E87 118d with the N47 diesel engine** (2007–2011), running in the browser and talking to the car through an ELM327 OBD-II adapter.

**Open it:** https://jmfreitas.github.io/bmwdash/

## Which car

Built and tuned for the **E87 118d · N47 (2.0 diesel)**. The header has a selector for:

| Setting | Car | Notes |
|---|---|---|
| E87 118d · N47 | 2007–2011 | main target |
| F20 118d · N47 | 2011–2015 | same engine, newer module list |
| F20/F40 118d · B47 | 2015+ | standard OBD only; DPF identifiers must be found with the identifier sweep |

Standard OBD gauges work on most cars, but the DPF and BMW module features assume a BMW with D-CAN (E-series from 03/2007 onwards).

## What it shows

- Speed and RPM gauges, a 60-second trend, and tiles for every sensor the car reports (coolant, boost, rail pressure, fuel rate, consumption…)
- **DPF panel**: regeneration status, the signals behind it, soot and ash mass, back pressure and status changes over time
- Standard OBD fault codes, and a BMW module scan with each module's own fault codes
- **Expert panel**: adapter check, raw console (read-only requests only), identifier sweep
- Trip log with CSV export, and copy buttons on every output box

## What you need

- **An ELM327 adapter that really implements its commands.** BMW module access needs `ATSH`, `ATCAF0`, `ATCRA` and ideally `ATCEA`. Many cheap "v2.1" clones reply OK to these without doing them; ones built on a **PIC18F25K80** chip (v1.5) or a vLinker/OBDLink work. Use **Check adapter** to find out.
- **Bluetooth or USB.** Wi-Fi adapters can't be used from a browser.
- **A browser with Web Bluetooth / Web Serial:**
  - Windows, Mac, Linux: Chrome or Edge. Pair a classic-Bluetooth adapter in system settings first, then use **Connect Serial / Classic BT**.
  - Android: Chrome 137 or newer, same buttons.
  - iPhone: not supported (Safari has no Bluetooth for web pages, and iOS blocks classic-Bluetooth serial adapters).

Try **Demo** first to see everything working with simulated data.

## Notes and safety

- BMW module requests are limited to read services; anything that writes, codes or resets is blocked. The only write action is **Clear codes** for standard OBD, which asks first.
- The N47 DPF identifiers come from community research; BMW doesn't publish their scaling, so those values are shown raw.
- Don't operate the dashboard while driving.

## Development

Everything lives in a single file, `index.html`, with no build step. Pushing to `main` publishes it to GitHub Pages via `.github/workflows/pages.yml`.

## License

GPL-3.0, see [LICENSE](LICENSE).
