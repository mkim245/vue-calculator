# vue-calculator

Single page Vue application calculator. This project was carried out to make an advanced calculator with the addition of new features to a simple calculator project (https://github.com/codyseibert/vue-calculator)

## User Instruction
### Basic keys
  - It has eleven number keys : 0, 00, 1, 2, 3, 4, 5, 6, 7, 8, 9
  - It has five operator keys : +, -, x, ÷, =
  - It has preset function keys : logarithm(Log), exponent(Exp), cubed(n³), reciprocal(1/n), square root(√), factorial(n!), percent(%), base of the natural logarithm(e), change of postive and negative sign(+/-), decimal(.)
  - It has editing keys : delete(DEL), clear(AC)

### key features
  - double layers are used to show operands and operators
  - press number -> operator -> number -> equal, display result (1 + 1 = 2)
  - press number -> operator -> equal, display result (10 + = 20)
  - press number -> preset function key, display result (2 % 0.02)
  - press operator in the presence of displayed result to continue calcuation (1 + 1 = 2 + 3 = 5)
  - press number in the presence of displayed result to start a new calcuation

## Screenshots

!["Initial image"](https://github.com/mkim245/vue-calculator/blob/master/public/screenshots/initial_image.PNG?raw=true)

!["First Number"](https://github.com/mkim245/vue-calculator/blob/master/public/screenshots/firstNumber.PNG?raw=true)

!["Operator"](https://github.com/mkim245/vue-calculator/blob/master/public/screenshots/operator.PNG?raw=true)

!["Second Number"](https://github.com/mkim245/vue-calculator/blob/master/public/screenshots/secondNumber.PNG?raw=true)

!["Answer"](https://github.com/mkim245/vue-calculator/blob/master/public/screenshots/results.PNG?raw=true)

## Project Stack

  - JavaScript, Vue

## Dependencies
  - "pinia": "^2.0.23",
  - "vue": "^3.2.41",
  - "vue-router": "^4.1.5"