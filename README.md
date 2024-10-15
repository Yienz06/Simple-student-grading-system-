def get_grade(score):
    if score >= 85:
        return 'A'
    elif score >= 70:
        return 'B'
    elif score >= 60:
        return 'C'
    elif score >= 50:
        return 'D'
    elif score >= 40:
        return 'E'
    else:
        return 'F'

def display_menu():
    print("\nWelcome to the Simple Grading System: ")
    print("1. Add student's detail")
    print("2. Display report analysis")
    print("3. Show average score and grade")
    print("4. Exit")

def calculate_average(scores):
    total_score = sum(scores)
    average_score = total_score / len(scores)
    return average_score

def grading_system():
    students = []  # student list initialized here

    choice = ''
    while choice != '4':
        display_menu()
        choice = input("Choose an option (1-4): ")

        if choice == '1':
            student_name = input("Enter student's name: ")
            num_scores = int(input(f"How many scores do you want to enter for {student_name}? "))
            scores = []

            for i in range(num_scores):
                score = float(input(f"Enter score {i + 1}: "))
                while score < 0.0 or score > 100.0:
                    print("Error: Score must be between 0 and 100.")
                    score = float(input(f"Re-enter score {i + 1}: "))
                scores.append(score)

            average_score = calculate_average(scores)
            grade = get_grade(average_score)
            students.append({'name': student_name, 'score': average_score, 'grade': grade})

            print(f"Student: {student_name}, Score: {average_score:.2f}, Grade: {grade}")

        elif choice == '2':
            if len(students) == 0:
                print("No student data available.")
            else:
                for student in students:
                    print(f"Student: {student['name']}, Score: {student['score']:.2f}, Grade: {student['grade']}")

        elif choice == '3':
            if len(students) == 0:
                print("No student data available to calculate the average.")
            else:
                total_score = sum(student['score'] for student in students)
                overall_average = total_score / len(students)
                overall_grade = get_grade(overall_average)
                print(f"Overall Average Score: {overall_average:.2f}, Overall Grade: {overall_grade}")

        elif choice == '4':
            print("Exiting the grading system. Goodbye!")
            break

        else:
            print("Invalid option! Please choose a number between 1 and 4.")

grading_system()
