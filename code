import tkinter as tk
from tkinter import simpledialog, messagebox

class TaskManager:
    def __init__(self, filename):
        self.tasks = []
        self.filename = filename
        self.load_tasks()

    def add_task(self, description):
        task = Task(description)
        self.tasks.append(task)
        self.save_tasks()

    def edit_task(self, index, description):
        try:
            self.tasks[index].description = description
            self.save_tasks()
        except IndexError:
            messagebox.showerror("Error", "Invalid task index")

    def delete_task(self, index):
        try:
            del self.tasks[index]
            self.save_tasks()
        except IndexError:
            messagebox.showerror("Error", "Invalid task index")

    def mark_task_as_complete(self, index):
        try:
            self.tasks[index].mark_as_complete()
            self.save_tasks()
        except IndexError:
            messagebox.showerror("Error", "Invalid task index")

    def display_tasks(self):
        for i, task in enumerate(self.tasks):
            print(f"{i+1}. {task}")

    def save_tasks(self):
        with open(self.filename, "w") as file:
            for task in self.tasks:
                file.write(f"{task.description},{task.completed}\n")

    def load_tasks(self):
        try:
            with open(self.filename, "r") as file:
                for line in file:
                    description, completed = line.strip().split(",")
                    task = Task(description)
                    task.completed = completed == "True"
                    self.tasks.append(task)
        except FileNotFoundError:
            pass

class Task:
    def __init__(self, description):
        self.description = description
        self.completed = False

    def mark_as_complete(self):
        self.completed = True

    def __str__(self):
        status = "Completed" if self.completed else "Incomplete"
        return f"{self.description} - {status}"

class TaskManagerGUI:
    def __init__(self, filename):
        self.task_manager = TaskManager(filename)
        self.window = tk.Tk()
        self.window.title("Task Manager")
        self.window.geometry("500x500")
        self.window.configure(background="#f0f0f0")  # light gray background

        self.task_listbox = tk.Listbox(self.window, width=40, font=("Arial", 14), bg="#e0e0e0")  # light gray background
        self.task_listbox.pack(pady=20)

        self.add_button = tk.Button(self.window, text="Add Task", command=self.add_task_callback, font=("Arial", 14), bg="#4CAF50", fg="white")  # green button
        self.add_button.pack(pady=10)

        self.edit_button = tk.Button(self.window, text="Edit Task", command=self.edit_task_callback, font=("Arial", 14), bg="#03A9F4", fg="white")  # blue button
        self.edit_button.pack(pady=10)

        self.delete_button = tk.Button(self.window, text="Delete Task", command=self.delete_task_callback, font=("Arial", 14), bg="#FF0000", fg="white")  # red button
        self.delete_button.pack(pady=10)

        self.mark_complete_button = tk.Button(self.window, text="Mark Task as Complete", command=self.mark_task_as_complete_callback, font=("Arial", 14), bg="#8BC34A", fg="white")  # green button
        self.mark_complete_button.pack(pady=10)

        self.display_tasks()

    def display_tasks(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.task_manager.tasks:
            self.task_listbox.insert(tk.END, str(task))

    def add_task_callback(self):
        description = simpledialog.askstring("Add Task", "Enter task description")
        if description:
            self.task_manager.add_task(description)
            self.display_tasks()

    def edit_task_callback(self):
        index = simpledialog.askinteger("Edit Task", "Enter task index")
        if index:
            description = simpledialog.askstring("Edit Task", "Enter new task description")
            if description:
                self.task_manager.edit_task(index - 1, description)
                self.display_tasks()

    def delete_task_callback(self):
        index = simpledialog.askinteger("Delete Task", "Enter task index")
        if index:
            self.task_manager.delete_task(index - 1)
            self.display_tasks()

    def mark_task_as_complete_callback(self):
        index = simpledialog.askinteger("Mark Task as Complete", "Enter task index")
        if index:
            self.task_manager.mark_task_as_complete(index - 1)
            self.display_tasks()

    def run(self):
        self.window.mainloop()

if __name__ == "__main__":
    task_manager_gui = TaskManagerGUI("tasks.txt")
    task_manager_gui.run()
