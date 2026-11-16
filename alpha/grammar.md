# Expression language

An alpha is one expression evaluated for every instrument in its universe on every day. The value is the signal; the weights setting turns it into a book.

## Text form

```
expr     := compare
compare  := sum (( ">" | "<" | ">=" | "<=" | "==" ) sum)?
sum      := term (( "+" | "-" ) term)*
term     := unary (( "*" | "/" ) unary)*
unary    := "-" unary | primary
primary  := number | "(" expr ")" | name | call
call     := name "(" arg ("," arg)* ")"
arg      := expr | number | "\"" text "\"" | key "=" (number | "\"" text "\"")
name     := close | volume | open_interest | <metric from the data sheet>
```

```
rank(ts_zscore(ret(20), 60) / vol(60))
```

Keyword arguments name optional parameters, for example `winsorize(x, std=3)` and `threshold(x, above=0.5)`. Strings are double-quoted: `odds("<market id>")`, `obs("fred.DGS10", "_")`. Errors point at the column.

## JSON form

Every text expression has one JSON tree. Either form is accepted wherever an expression is.

```json
{
  "op": "rank",
  "x": {
    "op": "div",
    "a": {
      "op": "ts_zscore",
      "x": {
        "op": "ret",
        "days": 20
      },
      "days": 60
    },
    "b": {
      "op": "vol",
      "days": 60
    }
  },
  "by": "universe"
}
```
