# You Don't Know JS: Scope & Closures
# Chapter 2: Lexical Scope

Javascript has lexical scope, not dynamic scope : the variable lookup is based on how scopes are visually contained inside each other in the code rather than the call stack (see appendix A).

## Lex-time

Lexical scope is defined by the lexer.

`eval` and `with` can break the lexical scope but we should not use them, also they make the code less performant since static code anaylisis optimisations become obsolettes.
