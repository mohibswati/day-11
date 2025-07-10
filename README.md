import os

class Employee:
    def __init__(self, name, department, salary, joining_year):
        self.name = name
        self.department = department
        self.salary = salary
        self.joining_year = joining_year

    def show(self):
        print(f"Name: {self.name}, Department: {self.department}, Salary: Rs.{self.salary}, Year: {self.joining_year}")

def load_data(file_name):
    data = []
    if os.path.exists(file_name):
        with open(file_name, 'r') as file:
            for line in file:
                name, dept, salary, year = line.strip().split(',')
                data.append(Employee(name, dept, float(salary), int(year)))
    return data

def save_data(file_name, data):
    with open(file_name, 'w') as file:
        for emp in data:
            file.write(f"{emp.name},{emp.department},{emp.salary},{emp.joining_year}\n")

def menu():
    file_name = "employee_data.txt"
    emp_list = load_data(file_name)

    while True:
        print("\n--- Employee System ---")
        print("1. Add Employee")
        print("2. Show All")
        print("3. Search")
        print("4. Sort by Salary")
        print("5. Exit")
        ch = input("Enter your choice: ")

        if ch == '1':
            name = input("Enter name: ")
            dept = input("Enter department: ")
            salary = float(input("Enter salary (PKR): "))
            year = int(input("Enter joining year: "))
            emp_list.append(Employee(name, dept, salary, year))
            save_data(file_name, emp_list)
            print("Employee added successfully.")

        elif ch == '2':
            if not emp_list:
                print("No data found.")
            for emp in emp_list:
                emp.show()

        elif ch == '3':
            search = input("Enter name or department to search: ").lower()
            results = [emp for emp in emp_list if search in emp.name.lower() or search in emp.department.lower()]
            if results:
                for emp in results:
                    emp.show()
            else:
                print("Not found.")

        elif ch == '4':
            emp_list.sort(key=lambda x: x.salary)
            print("Sorted by Salary (Low to High):")
            for emp in emp_list:
                emp.show()

        elif ch == '5':
            print("Program band ho gaya.")
            break

        else:
            print("Invalid option. Try again.")

if __name__ == "__main__":
    menu()


