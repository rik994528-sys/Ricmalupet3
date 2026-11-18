‎import os
‎import sys
‎import time
‎
‎MENU = {
‎    "A": "Lesson 1 - Introduction to Programming and Python",
‎    "B": "Lesson 2 - Understanding Python Syntax",
‎    "C": "Lesson 3 - Exploring Arithmetic Operators",
‎    "D": "Lesson 4 - Python Input and Output",
‎    "E": "Lesson 5 - Making Decisions With Conditional Statements",
‎    "F": "Lesson 6 - Understanding Logical Operators",
‎    "G": "Lesson 7 - Repeating Tasks with Loops",
‎    "H": "Quiz - Test What You Learned (10 Questions, 10 Seconds Each)",
‎}
‎
‎LESSONS = {
‎    "A": [
‎        "**What is a Programming Language**",
‎        "",
‎        "A programming language is a special language that computers understand and use to perform tasks.",
‎        "",
‎        "**What is Python Programming**",
‎        "",
‎        "Python is a widely used programming language that was created by Guido van Rossum in 1991.",
‎        "",
‎        "Guido van Rossum is a Dutch software engineer best known for creating Python.",
‎        "",
‎        "Python is a high level, interpreted, and general purpose programming language designed to be simple, readable, and easy to learn.",
‎        "",
‎        "**Why Learn Python**",
‎        "",
‎        "- It has simple, English-like syntax that is easy for beginners.",
‎        "- It is used in web development, data science, AI, games, and automation.",
‎        "- It has a huge community and many free libraries.",
‎    ],
‎    "B": [
‎        "**What is Syntax**",
‎        "",
‎        "Syntax is the set of rules that defines how a Python program must be written.",
‎        "",
‎        "**Indentation**",
‎        "",
‎        "Python uses indentation (spaces at the start of a line) to group code. Blocks such as if statements and loops must be indented.",
‎        "",
‎        "**Comments**",
‎        "",
‎        "A comment starts with # and is ignored by Python. Comments explain your code to people.",
‎        "Example: # This is a comment",
‎        "",
‎        "**Variables**",
‎        "",
‎        "A variable stores a value. You create one by assigning a value with =.",
‎        "Example: name = 'Ric'",
‎        "Example: age = 20",
‎        "",
‎        "**Case Sensitivity**",
‎        "",
‎        "Python is case sensitive. Name and name are two different variables.",
‎        "",
‎        "**Variable Naming Rules**",
‎        "",
‎        "- Must start with a letter or underscore, not a number.",
‎        "- Can only contain letters, numbers, and underscores.",
‎        "- Cannot be a Python keyword such as if, for, or while.",
‎        "",
‎        "**Common Data Types**",
‎        "",
‎        "- str  : text, such as 'Hello'",
‎        "- int  : whole numbers, such as 10",
‎        "- float: decimal numbers, such as 3.14",
‎        "- bool : True or False",
‎    ],
‎    "C": [
‎        "**What are Arithmetic Operators**",
‎        "",
‎        "Arithmetic operators are symbols used to do math in Python.",
‎        "",
‎        "**The Operators**",
‎        "",
‎        "+   Addition         10 + 3  = 13",
‎        "-   Subtraction      10 - 3  = 7",
‎        "*   Multiplication   10 * 3  = 30",
‎        "/   Division         10 / 3  = 3.3333 (always gives a float)",
‎        "//  Floor Division   10 // 3 = 3 (drops the decimal part)",
‎        "%   Modulus          10 % 3  = 1 (the remainder)",
‎        "**  Exponent         10 ** 3 = 1000 (power of)",
‎        "",
‎        "**Order of Operations**",
‎        "",
‎        "Python follows PEMDAS: Parentheses, Exponents, Multiplication and Division, then Addition and Subtraction.",
‎        "Example: 2 + 3 * 4 = 14",
‎        "Example: (2 + 3) * 4 = 20",
‎        "",
‎        "**Useful Tip**",
‎        "",
‎        "The modulus operator is often used to check if a number is even or odd. If number % 2 == 0, the number is even.",
‎        "",
‎        "**Shortcut Operators**",
‎        "",
‎        "x += 5 is the same as x = x + 5. This also works with -=, *=, and /=.",
‎    ],
‎    "D": [
‎        "**Output with print()**",
‎        "",
‎        "The print() function displays text or values on the screen.",
‎        "Example: print('Hello, World!')",
‎        "",
‎        "**Input with input()**",
‎        "",
‎        "The input() function asks the user to type something and returns what they typed.",
‎        "Example: name = input('Enter your name: ')",
‎        "",
‎        "**Input is Always Text**",
‎        "",
‎        "Everything returned by input() is a string, even if the user types a number. To do math, convert it first:",
‎        "age = int(input('Enter your age: '))",
‎        "price = float(input('Enter a price: '))",
‎        "",
‎        "**Combining Text and Variables**",
‎        "",
‎        "An f-string lets you place variables inside text.",
‎        "Example: print(f'Hello {name}, you are {age} years old')",
‎        "",
‎        "**Special Characters**",
‎        "",
‎        "\\n starts a new line.",
‎        "\\t adds a tab space.",
‎        "",
‎        "**Useful print() Options**",
‎        "",
‎        "- sep changes what goes between items: print('A', 'B', sep='-') shows A-B",
‎        "- end changes what goes at the end: print('Hi', end=' ') stays on the same line",
‎        "",
‎        "**Useful String Methods**",
‎        "",
‎        "- .upper() makes text uppercase",
‎        "- .lower() makes text lowercase",
‎        "- .strip() removes extra spaces at the start and end",
‎    ],
‎    "E": [
‎        "**What are Conditional Statements**",
‎        "",
‎        "Conditional statements let your program make decisions and run different code depending on a condition.",
‎        "",
‎        "**The if Statement**",
‎        "",
‎        "Runs code only if the condition is True.",
‎        "Example:",
‎        "    if age >= 18:",
‎        "        print('You are an adult')",
‎        "",
‎        "**The else Statement**",
‎        "",
‎        "Runs when the if condition is False.",
‎        "Example:",
‎        "    if age >= 18:",
‎        "        print('Adult')",
‎        "    else:",
‎        "        print('Minor')",
‎        "",
‎        "**The elif Statement**",
‎        "",
‎        "Short for else if. It checks another condition when the first one is False.",
‎        "Example:",
‎        "    if score >= 90:",
‎        "        print('A')",
‎        "    elif score >= 80:",
‎        "        print('B')",
‎        "    else:",
‎        "        print('Keep trying')",
‎        "",
‎        "**Comparison Operators**",
‎        "",
‎        "==  equal to",
‎        "!=  not equal to",
‎        "<   less than",
‎        ">   greater than",
‎        "<=  less than or equal to",
‎        ">=  greater than or equal to",
‎        "",
‎        "**Important Notes**",
‎        "",
‎        "- Use == to compare and = to assign.",
‎        "- Don't forget the colon : after the condition.",
‎        "- The code inside must be indented.",
‎    ],
‎    "F": [
‎        "**What are Logical Operators**",
‎        "",
‎        "Logical operators combine or change conditions. They return True or False.",
‎        "",
‎        "**and**",
‎        "",
‎        "True only if BOTH conditions are True.",
‎        "Example: age >= 18 and has_id",
‎        "True and True   = True",
‎        "True and False  = False",
‎        "False and False = False",
‎        "",
‎        "**or**",
‎        "",
‎        "True if AT LEAST ONE condition is True.",
‎        "Example: day == 'Saturday' or day == 'Sunday'",
‎        "True or False   = True",
‎        "False or False  = False",
‎        "",
‎        "**not**",
‎        "",
‎        "Reverses the result.",
‎        "Example: not is_raining",
‎        "not True  = False",
‎        "not False = True",
‎        "",
‎        "**Using Them in if Statements**",
‎        "",
‎        "    if age >= 18 and age <= 60:",
‎        "        print('Working age')",
‎        "",
‎        "**Order of Evaluation**",
‎        "",
‎        "Python checks not first, then and, then or. Use parentheses to make your meaning clear.",
‎        "",
‎        "**Short Circuiting**",
‎        "",
‎        "With and, if the first condition is False, Python skips the second one. With or, if the first is True, Python skips the second one.",
‎    ],
‎    "G": [
‎        "**What are Loops**",
‎        "",
‎        "A loop repeats a block of code so you don't have to write it many times.",
‎        "",
‎        "**The for Loop**",
‎        "",
‎        "Repeats code a set number of times or for each item in a sequence.",
‎        "Example:",
‎        "    for i in range(5):",
‎        "        print(i)",
‎        "This prints 0 1 2 3 4.",
‎        "",
‎        "**The range() Function**",
‎        "",
‎        "- range(5) gives 0 to 4",
‎        "- range(1, 6) gives 1 to 5",
‎        "- range(0, 10, 2) gives 0, 2, 4, 6, 8 (steps of 2)",
‎        "",
‎        "**The while Loop**",
‎        "",
‎        "Repeats as long as a condition is True.",
‎        "Example:",
‎        "    count = 1",
‎        "    while count <= 5:",
‎        "        print(count)",
‎        "        count += 1",
‎        "",
‎        "**Warning: Infinite Loops**",
‎        "",
‎        "If the condition never becomes False, the loop never stops. Make sure something inside the loop changes the condition.",
‎        "",
‎        "**break and continue**",
‎        "",
‎        "- break stops the loop immediately.",
‎        "- continue skips the rest of the current round and goes to the next one.",
‎        "",
‎        "**Looping Through Text**",
‎        "",
‎        "    for letter in 'Python':",
‎        "        print(letter)",
‎        "",
‎        "**Tip**",
‎        "",
‎        "Use a for loop when you know how many times to repeat. Use a while loop when you repeat until something happens.",
‎    ],
‎}
‎
‎codes = list(LESSONS.keys())
‎
‎TIME_LIMIT = 10
‎
‎QUIZ = [
‎    {"question": "Who created Python?",
‎     "options": ["Guido van Rossum", "Bill Gates", "Linus Torvalds", "Elon Musk"],
‎     "answer": "A"},
‎    {"question": "Which symbol starts a comment in Python?",
‎     "options": ["//", "#", "/*", "--"],
‎     "answer": "B"},
‎    {"question": "Which data type is 3.14?",
‎     "options": ["int", "str", "float", "bool"],
‎     "answer": "C"},
‎    {"question": "What is 10 % 3?",
‎     "options": ["3.33", "0", "3", "1"],
‎     "answer": "D"},
‎    {"question": "What is 2 + 3 * 4?",
‎     "options": ["20", "24", "14", "9"],
‎     "answer": "C"},
‎    {"question": "What type of data does input() always return?",
‎     "options": ["int", "str", "float", "bool"],
‎     "answer": "B"},
‎    {"question": "What lets you place variables inside text, like f'Hi {name}'?",
‎     "options": ["A comment", "An f-string", "A loop", "Modulus"],
‎     "answer": "B"},
‎    {"question": "Which keyword checks another condition after an if?",
‎     "options": ["else", "then", "switch", "elif"],
‎     "answer": "D"},
‎    {"question": "What is the result of True and False?",
‎     "options": ["True", "Error", "False", "None"],
‎     "answer": "C"},
‎    {"question": "What numbers does range(5) give?",
‎     "options": ["1 to 5", "0 to 5", "Only 5", "0 to 4"],
‎     "answer": "D"},
‎]
‎
‎
‎def timed_input(prompt, seconds):
‎    print(prompt, end="", flush=True)
‎    answer = ""
‎
‎    if os.name == "nt":
‎        import msvcrt
‎        while msvcrt.kbhit():
‎            msvcrt.getwch()
‎        end_time = time.time() + seconds
‎        while time.time() < end_time:
‎            if msvcrt.kbhit():
‎                ch = msvcrt.getwch()
‎                if ch in ("\r", "\n"):
‎                    print()
‎                    return answer
‎                elif ch == "\b":
‎                    if answer:
‎                        answer = answer[:-1]
‎                        print("\b \b", end="", flush=True)
‎                elif ch == "\x03":
‎                    raise KeyboardInterrupt
‎                else:
‎                    answer += ch
‎                    print(ch, end="", flush=True)
‎            time.sleep(0.05)
‎        print()
‎        return None
‎    else:
‎        import select
‎        ready, _, _ = select.select([sys.stdin], [], [], seconds)
‎        if ready:
‎            return sys.stdin.readline().strip()
‎        print()
‎        return None
‎
‎
‎def run_quiz():
‎    score = 0
‎    print()
‎    print("=" * 50)
‎    print("QUIZ TIME!")
‎    print("=" * 50)
‎    print(f"{len(QUIZ)} questions, {TIME_LIMIT} seconds each.")
‎    print("Type A, B, C or D, then press Enter.")
‎    input("\nPress Enter to start...")
‎
‎    for number, item in enumerate(QUIZ, start=1):
‎        print(f"\nQuestion {number}/{len(QUIZ)}")
‎        print(item["question"])
‎        for letter, text in zip("ABCD", item["options"]):
‎            print(f"  [{letter}] {text}")
‎
‎        answer = timed_input(f"\nYour answer ({TIME_LIMIT} seconds): ", TIME_LIMIT)
‎
‎        if answer is None:
‎            print(f"Time's up! The answer was {item['answer']}.")
‎        elif answer.strip().upper() == item["answer"]:
‎            print("Correct!")
‎            score += 1
‎        else:
‎            print(f"Wrong! The answer was {item['answer']}.")
‎
‎    print()
‎    print("=" * 50)
‎    print(f"Your score: {score}/{len(QUIZ)}")
‎    if score == len(QUIZ):
‎        print("Perfect score! Amazing!")
‎    elif score >= 7:
‎        print("Great job!")
‎    elif score >= 5:
‎        print("Not bad, review the lessons and try again!")
‎    else:
‎        print("Keep studying, you can do it!")
‎    print("=" * 50)
‎    input("\nPress Enter to go back to the Main Menu...")
‎
‎
‎def show_menu():
‎    print()
‎    for code, title in MENU.items():
‎        print(f"[{code}] {title}")
‎    print()
‎
‎
‎def show_lesson(code):
‎    print()
‎    print("=" * 50)
‎    print(MENU[code])
‎    print("=" * 50)
‎    print()
‎    for line in LESSONS[code]:
‎        print(line)
‎
‎
‎running = True
‎while running:
‎    show_menu()
‎    lesson_code = input("Please enter a lesson code: ").upper()
‎
‎    if lesson_code not in MENU:
‎        print("\nPlease enter a valid lesson code!")
‎        continue
‎
‎    if lesson_code == "H":
‎        run_quiz()
‎        continue
‎
‎    while True:
‎        show_lesson(lesson_code)
‎
‎        is_last = codes.index(lesson_code) == len(codes) - 1
‎        if is_last:
‎            print("\n[1] Finish (Back to Main Menu)")
‎        else:
‎            print("\n[1] Continue to Next Lesson")
‎        print("[2] Go Back to Main Menu")
‎        print("[3] Exit")
‎        choice = input("\nPlease enter a choice: ")
‎
‎        if choice == "1":
‎            if is_last:
‎                print("\nCongratulations, you finished all lessons! Returning to Main Menu...")
‎                break
‎            lesson_code = codes[codes.index(lesson_code) + 1]
‎            print("\nMoving to the next lesson...")
‎        elif choice == "2":
‎            print("\nReturning to Main Menu...")
‎            break
‎        elif choice == "3":
‎            print("\nThank you for studying!")
‎            running = False
‎            break
‎        else:
‎            print("\nPlease enter a valid choice!")
‎
