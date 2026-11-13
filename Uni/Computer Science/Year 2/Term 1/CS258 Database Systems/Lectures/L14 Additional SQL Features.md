
## Outline:

- Window functions
- Time/ Date conversions
- Procedural


## Converting Times to INTEGERs

Timestamp contains multiple components that can be extracted

In where now() gives 
e.g 
year FROM now() - the year your are currently in
epoch FROM now() - the time you are currently in


``` SQL
SELECT CAST(extract(epoch from now()) AS INTEGER);
```

This command performs the same thing as epoch from now() however it strips away the decimal places by converting it into an Integer.

## Window Functions

