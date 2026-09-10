# Ancillary Services Insights by Jacob's Code

Forecasts for Swedish day-ahead spot and reserve markets, issued before each market gate. This folder holds
data only.

* `proofs/<date>/<issue>.json` is published at issue time: the sha256 of the forecast file and an RFC 3161
  timestamp reply (`.tsr`) from a public timestamping authority, whose clock attests when the hash existed.
* `forecasts/<date>/<issue>.csv` is released after the delivery day has passed. Hash it and compare:

```
shasum -a 256 forecasts/2026-09-09/spot.csv
openssl ts -verify -data forecasts/2026-09-09/spot.csv -in proofs/2026-09-09/spot.csv.tsr -CAfile freetsa_cacert.pem
```

Columns: series, target hour (UTC and local), horizon, forecast, P10/P90, whether the hour was already
published at issue time (those hours are not forecasts and are not scored), and the same-as-yesterday
baseline. `index.html` is the scoreboard.
