
## Callback applied to every found solution

>So after a lot of digging through the source code and experimenting, I found out how to do this! The documentation is very sparse and not particularly helpful on this issue, I mostly pieced it together from the existence of various functions. Basically I needed to create a callback that could be passed to the solver using `routing_model.AddAtSolutionCallback(routing_monitor)`. The callback is just a class where the `__call__` function is what is executed at each solution. This function defines a class with a tolerance for the number of consecutive failures, and if those failures occur, it tells the solver to finish and return what it has.

```python
def make_routing_monitor(routing_model: pywrapcp.RoutingModel, failure_limit: int) -> callable:
    class RoutingMonitor:
        def __init__(self, model: pywrapcp.RoutingModel):
            self.model = model
            self._counter = 0
            self._best_objective = inf
            self._counter_limit = failure_limit

        def __call__(self):
            self._best_objective = min(self._best_objective, self.model.CostVar().Max())
            if self._best_objective == self.model.CostVar().Max():
                self._counter = 0
            else:
                self._counter += 1
                if self._counter > self._counter_limit:
                    self.model.solver().FinishCurrentSearch()
    return RoutingMonitor(routing_model)
```
Source: https://github.com/google/or-tools/issues/1439