# Timers must be Drained to Reset

Timers in go expose a public channel. If the timer is created via `NewTimer` and
the timer needs to be reset, the channel must be drained.

# Reset a timer


```go
  if !t.Stop() {

    <-t.C

  }

  t.Reset(d)
```

I find that the best way to handle this condition it to keep the scope of the
timer with the go routine that created it, instead of draining and coordinating
that drain from another routine.
