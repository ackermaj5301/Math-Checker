# Math-Checker
Math Checker Group Assignment
import re

def math_checker():
    print("Welcome to the Math Checker!")
    print("Enter your own math problem using +, -, *, or /")
    print("Numbers must be WHOLE numbers between 0 and 100.")
    print("Type 'exit' anytime to quit.\n")

    while True:
        problem = input("Enter your math problem (example: 25+36): ")

        if problem.lower() == "exit":
            print("Goodbye! Keep practicing your math!")
            break

        # Remove extra spaces
        problem = problem.replace(" ", "")

        # Use regex to split number/operator/number
        match = re.match(r"^(\d+)([+\-*/])(\d+)$", problem)
        if not match:
            print("❌ Please enter in format like 25+36 or 25 + 36 (whole numbers only).")
            continue

        num1, operator, num2 = match.groups()
        num1 = int(num1)
        num2 = int(num2)

        # Range check
        if not (0 <= num1 <= 100 and 0 <= num2 <= 100):
            print("❌ Numbers must be between 0 and 100.")
            continue

        # Compute correct answer
        if operator == '+':
            correct_answer = num1 + num2
        elif operator == '-':
            correct_answer = num1 - num2
        elif operator == '*':
            correct_answer = num1 * num2
        elif operator == '/':
            if num2 == 0:
                print("❌ Division by zero is not allowed.")
                continue
            if num1 % num2 != 0:  # must divide evenly
                print("❌ Division must result in a whole number.")
                continue
            correct_answer = num1 // num2

        # Ask student for their answer
        user_input = input(f"What answer did you get for {num1} {operator} {num2}? ")
        if user_input.lower() == "exit":
            print("Goodbye! Keep practicing your math!")
            break

        try:
            user_answer = int(user_input)  # whole number only
            if user_answer == correct_answer:
                print("✅ Correct! Great job!\n")
            else:
                print("❌ Incorrect, try again!\n")
        except ValueError:
            print("❌ Invalid input. Please enter a whole number.")

# Run it
math_checker()
