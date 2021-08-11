# Hurst Exponent (Preview)

The [Hurst Exponent](https://en.wikipedia.org/wiki/Hurst_exponent) is a [random-walk](https://en.wikipedia.org/wiki/Random_walk) path analysis that measures trending and mean-reverting tendencies of incremental return values.  When `H` is greater than 0.5 it depicts trending.  When `H` is less than 0.5 it is is more likely to revert to the mean.  When `H` is around 0.5 it represents a random walk.
[[Discuss] :speech_balloon:](https://github.com/DaveSkender/Stock.Indicators/discussions/477 "Community discussion about this indicator")

![image](chart.png)

```csharp
// usage
IEnumerable<HurstResult> results =
  quotes.GetHurst(lookbackPeriods);  
```

## Parameters

| name | type | notes
| -- |-- |--
| `lookbackPeriods` | int | Number of periods (`N`) in the Hurst Analysis.  Must be greater than 100.  Default is 100.

### Historical quotes requirements

You must have at least `N+1` periods of `quotes`.

`quotes` is an `IEnumerable<TQuote>` collection of historical price quotes.  It should have a consistent frequency (day, hour, minute, etc).  See [the Guide](../../docs/GUIDE.md#historical-quotes) for more information.

## Response

```csharp
IEnumerable<HurstResult>
```

The first `N` periods will have `null` values since there's not enough data to calculate.  We always return the same number of elements as there are in the historical quotes.

### HurstResult

| name | type | notes
| -- |-- |--
| `Date` | DateTime | Date
| `HurstExponent` | double | Hurst Exponent (`H`)

### Utilities

- [.ConvertToQuotes()](../../docs/UTILITIES.md#convert-to-quotes)
- [.Find(lookupDate)](../../docs/UTILITIES.md#find-indicator-result-by-date)
- [.RemoveWarmupPeriods()](../../docs/UTILITIES.md#remove-warmup-periods)
- [.RemoveWarmupPeriods(qty)](../../docs/UTILITIES.md#remove-warmup-periods)

See [Utilities and Helpers](../../docs/UTILITIES.md#content) for more information.

## Example

```csharp
// fetch historical quotes from your feed (your method)
IEnumerable<Quote> quotes = GetHistoryFromFeed("SPY");

// calculate 20-period Hurst
IEnumerable<HurstResult> results = quotes.GetHurst(20);
```