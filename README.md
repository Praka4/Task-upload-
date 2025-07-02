# Task-upload-
import json

# Load tasks from file or initialize
def load_tasks():
    try:
        with open("tasks.json", "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []

# Save tasks to file
def save_tasks(tasks):
    with open("tasks.json", "w") as file:
        json.dump(tasks, file)

# Display tasks
def view_tasks(tasks):
    if not tasks:
        print("No tasks found!")
    for idx, task in enumerate(tasks):
        status = "✓" if task['done'] else "✗"
        print(f"{idx + 1}. [{status}] {task['title']}")

# Add new task
def add_task(tasks):
    title = input("Enter task title: ")
    tasks.append({"title": title, "done": False})
    print("Task added!")

# Mark as done
def mark_done(tasks):
    view_tasks(tasks)
    try:
        num = int(input("Enter task number to mark as done: ")) - 1
        tasks[num]['done'] = True
        print("Task marked as done!")
    except:
        print("Invalid input!")

# Delete task
def delete_task(tasks):
    view_tasks(tasks)
    try:
        num = int(input("Enter task number to delete: ")) - 1
        tasks.pop(num)
        print("Task deleted!")
    except:
        print("Invalid input!")

# Main loop
def main():
    tasks = load_tasks()
    while True:
        print("\nTo-Do Manager")
        print("1. Add Task\n2. View Tasks\n3. Mark Task as Done\n4. Delete Task\n5. Exit")
        choice = input("Choose: ")
        if choice == '1':
            add_task(tasks)
        elif choice == '2':
            view_tasks(tasks)
        elif choice == '3':
            mark_done(tasks)
        elif choice == '4':
            delete_task(tasks)
        elif choice == '5':
            save_tasks(tasks)
            print("Goodbye!")
            break
        else:
            print("Invalid choice!")

main()
