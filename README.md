# TheStrat TTO: Triangle They Out

TheStrat TTO is a TradingView indicator (Pine Script v6) that automates the Triangle They Out, a pattern taught by Rob Smith, the creator of TheStrat. The name describes the setup: price forms a triangle, the move out of it stops out the traders positioned at its edge (it takes "them" out), and the entry comes after they are stopped out.

**On TradingView:** [TheStrat TTO: Triangle They Out (Stop Hunt Entries)](https://www.tradingview.com/script/qAsbbUqj-TheStrat-TTO-Triangle-They-Out-Stop-Hunt-Entries/), open source, by SpinTrades.

How the indicator reads it: a pullback leaves a point of structure. A later bar sweeps it, running the stops that sit beyond it, and closes back inside. The entry is a break of that sweep bar's opposite extreme, and the sweep extreme is where the stop goes.

It is display and alerts only: no orders, no strategy. It shows where the setup armed, where it triggered, and where it would be wrong.

## Reading the chart

| Mark | Meaning |
|---|---|
| Grey line | The swept structure, from the bar that made it to the sweep bar |
| Dotted green / red line | An armed setup's trigger. It runs right until the setup enters or dies; a faint end means it died untraded |
| Green / red triangle | Entry: price traded through the trigger. The text is the slot timeframe (`5m`, `15m`, `1H`). Hover it for the trigger, the stop reference and what `x2` means |
| `x2` on the triangle | Sweep of a sweep: the swept level was itself an older sweep extreme |
| Soft green / red box | The fair value gap that qualified the setup, labeled with its timeframe. Stacked boxes = gaps nested across timeframes. Off by default: turn on Draw qualifying gaps |

Green and red always mean bull and bear, never good and bad. The entry marker can be a triangle, arrow, label, diamond or circle, at any size, under Style.

## How a setup forms

Bullish shown; bearish is the mirror.

1. **Structure.** Every confirmed three-bar fractal low on a watched timeframe is remembered until it is broken, or swept and resolved. A newer low does not erase an older one.
2. **Flush.** A bar trades below a remembered low. The running low is the flush extreme.
3. **Reclaim.** Within the reclaim window (default 2 bars after the newest low), a close back above a swept low arms the setup on the deepest low reclaimed. Trigger = that bar's high. Stop reference = the flush extreme.
4. **Extension.** While armed, a deeper low that still closes above the level moves the trigger and stop reference to that bar.
5. **Kill.** A close back below the armed level ends it.
6. **Entry.** Price trades through the trigger.

## Timeframes

Four slots, set to 5m, 15m, 30m and 1H, each switchable and set to any timeframe. Only the 15m slot is on by default. Each slot runs its own detector on bars built from one stream at the finest slot, so the chart timeframe is only zoom: a 5m chart and a 15m chart show the same setups at the same times. Line width and triangle size grow with the slot's rank.

A slot above 30m that sits strictly between the finest slot and the chart timeframe can't be built honestly (session anchors break hourly clock math), so it switches off. The status tag lists it.

**Hide slots finer than the chart** (on by default): a slot shows its marks and sends its alerts only on charts at or below its own timeframe. With the default 15m slot, a 15m or finer chart shows it and a 1H or Daily chart shows none, so higher timeframes stay readable. Hidden slots keep running, so whatever a slot does show is identical on every chart. The status tag lists hidden slots.

## Filters

Filters hide marks and silence alerts. The detectors run unfiltered underneath, so turning a filter off never changes what the detector found.

- **Fair value gap** (on by default): the sweep extreme must sit inside a live same-direction gap on the setup's own timeframe or a higher one. A gap dies the moment price trades fully through it.
- **Timeframe continuity** (on by default, Daily): every enabled continuity timeframe must be on the trade's side of its open, at the sweep and again at the entry. Same rule as TheStrat Suite's FTFC.
- **ACT trend direction** (off by default): ACT (Alignment-Colored Trend) must read a trend in the setup's direction. Main trend: price above (below) the opens of both of the ladder's Direction timeframes, D and W on the Day Trade ladder. Counter-trend: those two disagree and the State 2 timeframe (4H) has broken up (down). Pick trend or counter-trend, or main trend only; no trend blocks both. ACT's logic is built in, so ACT does not need to be on the chart; if you run it, set the ladder to match.

With both default filters on, marks are deliberately sparse. Turn on Advanced > Mark filtered-out sweeps to see what was hidden and why (`tfc`, `act`, `young`, `gap`).

## Alerts

Create one alert on the indicator with the condition **Any alert() function call**. It carries every shown sweep and entry with the trigger and stop reference in the message, and respects every filter. Per-event conditions also exist for sweeps, entries, and sweeps of a sweep.

The status tag says which timing you have:

- **alerts live**: the chart's bars are the finest slot (a 15m chart with the default 15m slot). The entry alert fires the moment price crosses the trigger.
- **alerts bar close**: the chart is coarser. The alert comes at the chart bar's close.

## No repaint

Detector state advances on confirmed bars only, and closed bars never change. Entries are tested on every stream bar, so the triangle sits on the bar that actually crossed. With a filter on, a live alert reads the filter at the crossing and the marker reads it at the bar's close, so inside one bar the two can disagree. With every filter off they cannot.

## Limits

- Slot bars come from lower-timeframe data. Beyond the plan's intrabar depth, older chart bars have no stream and the indicator is quiet there.
- A setup that arms on a session's last slot bar resolves on the next session's open.
- Each shown setup draws two lines, and TradingView keeps the most recent 500, so very long histories lose their oldest marks.
- An entry bar that also trades through the stop reference is not marked differently yet.

## License

Mozilla Public License 2.0.
