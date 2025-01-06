# Task-Manager-Tool
# Step 1: Initialize Git Repository
mkdir TaskManagerTool
cd TaskManagerTool
git init

# Step 2: Create README.md and Commit
cat <<EOL > README.md
# Task Manager Tool

This project is a simple task manager tool that supports adding and deleting tasks.
EOL
git add README.md
git commit -m "Initial commit with README.md"

# Step 3: Create and Switch to Branches
git branch feature/add-tasks
git branch feature/delete-tasks

git checkout feature/add-tasks

# Step 4: Add Feature to Add Tasks
cat <<EOL > add_task.py
# add_task.py

def add_task(task_list, task):
    task_list.append(task)
    return task_list

if __name__ == "__main__":
    tasks = []
    task = input("Enter a task to add: ")
    tasks = add_task(tasks, task)
    print("Task added!", tasks)
EOL
git add add_task.py
git commit -m "Add feature to add tasks"

# Step 5: Switch to feature/delete-tasks and Add Delete Feature
git checkout feature/delete-tasks

cat <<EOL > delete_task.py
# delete_task.py

def delete_task(task_list, task):
    if task in task_list:
        task_list.remove(task)
    else:
        print("Task not found!")
    return task_list

if __name__ == "__main__":
    tasks = ["Task1", "Task2"]
    print("Current tasks:", tasks)
    task = input("Enter a task to delete: ")
    tasks = delete_task(tasks, task)
    print("Updated tasks:", tasks)
EOL
git add delete_task.py
git commit -m "Add feature to delete tasks"

# Step 6: Merge and Resolve Conflicts
## Merge feature/add-tasks into main
git checkout main
git merge feature/add-tasks

## Attempt to merge feature/delete-tasks into main
git merge feature/delete-tasks

# Conflict: Assume the README.md has conflicting changes
cat <<EOL > README.md
# Task Manager Tool

This project is a simple task manager tool that supports adding and deleting tasks.

## Features:
- Add tasks (feature/add-tasks)
- Delete tasks (feature/delete-tasks)
EOL

git add README.md
git commit -m "Resolve merge conflict in README.md"

# Step 7: Push Changes to Remote Repository (Optional)
git remote add origin git@github.com:username/TaskManagerTool.git
git push -u origin main
