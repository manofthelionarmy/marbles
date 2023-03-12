# Summary:
---
# Related Stuff:
#golang
#interpreters

---
# Notes:
- We need to transform our source code into something more accesible.
- The first step in an intepreter is to transform our source codes into tokens.
- This step is known as lexical analysis or lexing.
- This is done by a lexer, aka tokenizer.
- Tokens are small, easily categorizable data structuers that are fed to the parser, which does the second transformation and turns the tokens into an "Abstract Syntax Tree".
- Sometimes whitespace is tokenized, other times it is not. In this book, we'll ignore whitespace and not tokenize it.
- Therefore, when we create our lexer, our first step is define the tokens it is going to output.