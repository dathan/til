
# PROM types

* The officle resource on promql is the following [location](https://prometheus.io/docs/prometheus/latest/querying/basics/)

* In Prometheus's expression language, an expression or sub-expression can evaluate to one of four types:

```
Instant vector - a set of time series containing a single sample for each time series, all sharing the same timestamp
Range vector - a set of time series containing a range of data points over time for each time series
Scalar - a simple numeric floating point value
String - a simple string value; currently unused
```

* Instant Vectors are fetched by the metric name and can be filtered by adding label matches using curly braces 
```
{}
```

`e.g. http_requests_total{job="prometheus",group="canary"}`


* operators:
```
=: Select labels that are exactly equal to the provided string.
!=: Select labels that are not equal to the provided string.
=~: Select labels that regex-match the provided string.
!~: Select labels that do not regex-match the provided string.
```


* All regular expressions in Prometheus use [RE2 syntax](https://github.com/google/re2/wiki/Syntax)
* 
