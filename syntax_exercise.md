## Grammar
```
<code> -> begin <statement> end
<statement> -> <assign>; | <assign>; <statement>
<assign> -> <id> = <expr>
<id> -> A | B | C
<expr> -> <id> + <expr> | <id> * <expr> | ( <expr> ) | <id>
```

## Derivation
```
 <code> -> begin <statement> end
        -> begin <assign>; <statement> end
        -> begin <id> = <expr>; <statement> end
        -> begin B = <expr>; <statement> end
        -> begin B = <id> * <expr>; <statement> end
        -> begin B = C * <expr>; <statement> end
        -> begin B = C * <id> + <expr>; <statement> end
        -> begin B = C * A + <expr>; <statement> end
        -> begin B = C * A + <id> * <expr>; <statement> end
        -> begin B = C * A + B * <expr>; <statement> end
        -> begin B = C * A + B * <id>; <statement> end
        -> begin B = C * A + B * B; <statement> end
        -> begin B = C * A + B * B; <assign>; end
        -> begin B = C * A + B * B; <id> = <expr>; end
        -> begin B = C * A + B * B; C = <expr>; end
        -> begin B = C * A + B * B; C = ( <expr> ); end
        -> begin B = C * A + B * B; C = (<id> * <expr>); end
        -> begin B = C * A + B * B; C = (B * <expr>); end
        -> begin B = C * A + B * B; C = (B * <id> + <expr>); end
        -> begin B = C * A + B * B; C = (B * C + <expr>); end
        -> begin B = C * A + B * B; C = (B * C + <id>); end
        -> begin B = C * A + B * B; C = (B * C + A); end
```

## Parse Tree
![Parse Tree](https://user-images.githubusercontent.com/90940695/136701947-f58d5423-f227-42df-9d73-d1f71b4ce14b.png)
