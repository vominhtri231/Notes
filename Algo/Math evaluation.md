# Math evaluation

## Math notation

An Arithmetic Expression can be express as:

- Infix Notation: Operation are written between operand. Eg: `3 + 4`. This form is written and recognized by human but hard for computer to evaluate.
- Prefix Notation: Operation are written before: Eg: `+ 3 4`
- Postfix Notation: Operation are written after: Eg: `3 4 +`

## Shunting-yard algorithm

This is a algorithm for converting a infix notation to postfix notation. Here is its pseudo code:

- Initialize a operator stack and a output queue
- Foreach token, if token is
  - number: push to output queue
  - an operator: pop all operators from the operator stack that have the greater precedence than it into the output queue. Push the operator into the stack
  - Left parenthesis: push to the operator stack
  - Right parenthesis: pop all operator from the stack until find the left parenthesis into the output queue, discard the left parenthesis.
- Pop all operators from the operator stack into the output queue
