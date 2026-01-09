# Task-Tracker
A lightweight Command Line Interface (CLI) application built with Python to help users manage daily tasks. This project demonstrates basic CRUD (Create, Read, Update, Delete) operations and persistent data storage using text files.
import os

def display_menu():
    print("\n--- PERSONAL TASK TRACKER ---")
    print("1. View Tasks")
    print("2. Add Task")
    print("3. Remove Task")
    print("4. Exit")

def load_tasks():
    if not os.path.exists("tasks.txt"):
        return []
    with open("tasks.txt", "r") as file:
        return [line.strip() for line in file.readlines()]

def save_tasks(tasks):
    with open("tasks.txt", "w") as file:
        for task in tasks:
            file.write(task + "\n")

def main():
    tasks = load_tasks()
    while True:
        display_menu()
        choice = input("Choose an option (1-4): ")

        if choice == '1':
            print("\nYOUR TASKS:")
            if not tasks:
                print("No tasks found.")
            for i, task in enumerate(tasks, 1):
                print(f"{i}. {task}")
        
        elif choice == '2':
            new_task = input("Enter the task description: ")
            tasks.append(new_task)
            save_tasks(tasks)
            print("Task added!")

        elif choice == '3':
            if not tasks:
                print("Nothing to delete.")
                continue
            try:
                task_num = int(input("Enter task number to remove: "))
                removed = tasks.pop(task_num - 1)
                save_tasks(tasks)
                print(f"Removed: {removed}")
            except (ValueError, IndexError):
                print("Invalid number.")

        elif choice == '4':
            print("Goodbye!")
            break
        else:
            print("Invalid choice, try again.")

if _name_ == "_main_":
    main()

