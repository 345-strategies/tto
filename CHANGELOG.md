# Changelog

## 1.3.3 (2026-10-26)

- Draw qualifying gaps is off by default. The gap filter still runs; turn the setting on to see the boxes.

No change to detection, filters or alerts.

## 1.3.2 (2026-10-26)

- With the ACT filter off, TTO requests no ACT data. Above 1H the Auto ACT ladder asked for 3M and 12M bars even with the filter off, so TradingView's Pine Screener refused every symbol on 2H, 4H, daily and weekly scans. They now run with default settings.

No change to detection, filters or alerts.

## 1.3.1 (2026-10-23)

- Hovering an entry marker explains it: timeframe, direction, trigger, stop reference, and what x2 means.
- Script header credits Rob Smith and TheStrat for the Triangle They Out.

No change to detection, filters or alerts.

## 1.3.0 (2026-10-23)

First public release.

- Entry marker shape and size are selectable; entries from several timeframes on one bar share one marker.
- Slots finer than the chart are hidden by default, so higher-timeframe charts aren't buried in small-timeframe entries. One switch turns it off.

## 1.2.1 (2026-10-23)

- Settings regrouped, every input explained in a tooltip.
- Colors follow TheStrat Suite: bull #4caf50, bear #f23645, structure grey.
- Status tag can be hidden and moved.
- Timeframes read 5m / 1H / 4H on the chart and in alerts.

## 1.2.0 (2026-10-17)

- Optional filter by ACT candle direction, at the sweep and the entry.

## 1.1.0 (2026-10-17)

- One mark per trade: armed setups draw a dotted trigger line instead of an arrow, ending where the setup enters or dies.
- Swept-level line is neutral grey; sweep of a sweep shows as `x2` on the entry triangle.

## 1.0.0 (2026-09-01)

- Standalone entry tool: four timeframe slots, fair value gap and timeframe continuity filters, sweep of a sweep, entries tested at the crossing, live or bar-close alerts.
