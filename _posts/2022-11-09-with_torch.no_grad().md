# When will we use `with torch.no_grad()`?
If we don't want to build computational graph based on current result and backward propagation, we will use this code command.
All the deflault parameter set for `requires_grad` is `False`.
For example:
```python
    for i in range(10):
        loss = quad_mae(abc)
        loss.backward()
        with torch.no_grad(): abc -= abc.grad*0.01
        print(f'step={i}; loss={loss:.2f}')
```
> `abc -= abc.grad*0.01` isn't actually part of our quadratic model, so we don't want derivitives to include that calculation.