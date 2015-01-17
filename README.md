# StackExpressions
Evaluating an expression in Python using stacks

from my_stacks import *

class Stack:

    def evaluate(operand1, operator, operand2):
        '''(int, str, int) -> int
        Calculate and return the result of the mathematical expression operand, operator, operand.
        REQ operator is one of +-*/
        '''
        if(operator == '+'):
            result = operand1 + operand2
        elif(operator == '-'):
            result = operand1 - operand2
        elif(operator == '*'):
            result = operand1 * operand2
        else:
            result = operand1 / operand2
        return result
    
def eval_expr(expr):
    ''' (str) -> int
    Evaluate a fully parenthasized mathematical expression including addition, subtraction, multiplication, and division.
    REQ: all operands are single digit positive integers
    REQ: operands must all be one of +-*/
    REQ: must be fully paranthesized
    '''
    my_stack = Stack()
    for next_char in expr:
        if(next_char in '1234567890+-*/'):
            my_stack.push(next_char)
        elif(next_char == ')'):
            num2 = int(my_stack.pop())
            op = my_stack.pop()
            num1 = int(my_stack.pop())
            res = evaluate(num1, op, num2)
            my_stack.push(str(res))
    return int(my_stack.pop())

class EmptyStackError(Exception):
    'an error to raise when someone tries to pop from an empty stack.'
    
if(__name__ == '__main__'):
    
    try:
        print(eval_expr('(3 + 7)'))
    except KeyError:
        print('Tried to pop from an empty stack.')
              
