# <a href="https://Jaclem.github.io/index">Python</a> | C Programming | <a href="https://Jaclem.github.io/linux">Linux</a>

---

## Problem
Create a Calculator without using built in libraries and create your own functions that perform the actions in which libraries would normally take care of.
- [+] For Addition
- [-] For Subtraction
- [/] For Division
- [*] For Multiplication
- [^] The first number you enter will be to the power of the second number you enter
- [e] The first number you enter will be to the power of e
- [!] For the factorial of any integer
- [r] For any random number between two integers entered
- [s] To calculate the sum consecutive integers between two given integers
- [~] To round to the nearest integer given any decimal value
- [<] Determine the lesser of two values entered
- [>] Determine the greater of two values entered

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int round(double x);
float maximum(float x, float y);
float minimum(float x, float y);
float factorial(float x);
float exponential(int y);
void power(float x, int y);

main(void) {
	int min, max, n, sum;
	char operator, start;
	double numRound;
	float numberOne, numberTwo, total, factor, exp, e = 2.71828;


	puts("**********************************************************");
	puts("\nHere is a full list of the ones that you could use.\n");
	puts("+ For Addition");
	puts("- For Subtraction");
	puts("/ For Division");
	puts("* For Multiplication");
	puts("^ The first number you enter will be to the power of the second number you enter\n");
	puts("e The first number you enter will be to the power of e");
	puts("! For the factorial of any integer");
	puts("r For any random number between two integers entered");
	puts("s To calculate the sum consecutive integers between two given integers");
	puts("~ To round to the nearest integer given any decimal value");
	puts("< Determine the lesser of two values entered");
	puts("> Determine the greater of two values entered\n");
	puts("**********************************************************\n\n");

	printf("Enter y to start the program or n to close.\n");

	scanf_s("%c", &start);


	if (start == 'n')
	{
		printf("End.");
		return 0;
	}
	else if (start != 'y')
	{
		printf("ERROR: invalid selection.");
		return 0;
	}
	else if (start == 'y')
	{
		printf("Now enter an operator you would like to use and two numbers to be calculated by said operator.\n");
	}

	while (start == 'y')
	{
		scanf_s(" %c", &operator);

		if (operator == 'n')
		{
			printf("End program.\n");
			return 0;
		}

		if ((operator != '!') && (operator != 'e') && (operator != 'r') && (operator != '~'))
		{
			scanf_s("%f %f", &numberOne, &numberTwo);
		}

		switch (operator)
		{
		case '+':
			total = numberOne + numberTwo;
			printf("The result of adding those two numbers is %.2f\n", total);
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '-':
			total = numberOne - numberTwo;
			printf("The result of subtracting those two numbers is %.2f\n", total);
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '/':
			total = numberOne / numberTwo;
			printf("The result of dividing those two numbers is %.2f\n", total);
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '*':
			total = numberOne * numberTwo;
			printf("The result of multiplying those two numbers is %.2f\n", total);
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '>':
			printf("The greater number out of the two is %.2f\n", maximum(numberOne, numberTwo));
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '<':
			printf("The lesser number of the two is %.2f\n", minimum(numberOne, numberTwo));
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '^':
			power(numberOne, numberTwo);

			break;

		case 'e':
			scanf_s("%f", &exp);
			printf("The exponential is %f\n", exponential(exp));
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '!':
			scanf_s("%f", &factor);
			printf("The factorial number for %.2f is %.2f\n", factor, factorial(factor));
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case 'r':
			scanf_s("%d %d", &min, &max);

			srand(time(NULL));
			if (min < max)
			{
				printf("%d\n", (rand() % (min - max) + min));
			}
			else if (min > max)
			{
				printf("%d\n", (rand() % (max - min) + max));
			}
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case 's':
			n = numberTwo - numberOne + 1;
			sum = (numberOne + numberTwo) * n / 2;

			printf("%d\n", sum);
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		case '~':
			scanf_s("%lf", &numRound);

			printf("%d\n", round(numRound));
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;

		default:
			printf("ERROR: invalid operator chosen please choose a valid operator.\n");
			printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");

			break;
		}
	}
}

// function definitions
float maximum(float x, float y)
{
	float max = x;

	if (y > max)
	{
		max = y;
	}
	if (x > max)
	{
		max = x;
	}

	return max;
}

float minimum(float x, float y)
{
	float min = x;

	if (y > min)
	{
		min = x;
	}
	if (y < min)
	{
		min = y;
	}

	return min;
}

void power(float x, int y)
{
	float power = x;
	int firstNum = y;

	while (y >= 2)
	{
		power *= x;
		y--;
	}
	printf("%.2f to the power of %d is %.2f\n\n", x, firstNum, power);
	printf("Now enter another operator and two more numbers that you would like calculated (n to end).\n");
}

float factorial(float x)
{
	int counter = 1;
	int fact = 1;

	while (counter < x)
	{
		counter++;
		fact = counter * fact;
	}

	return fact;
}

float exponential(int y)
{
	float e = 2.71828, exp = e;

	while (y >= 2)
	{
		exp *= e;
		y--;
	}

	return exp;
}

int round(double x)
{
	double numRound = x;
	int decimalNum = numRound >= 0 ? (int)(numRound + 0.5) : (int)(numRound - 0.5);

	return decimalNum;
}
```
