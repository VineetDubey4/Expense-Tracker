# Expense-Tracker

import csv
from datetime import datetime

FILENAME = "expenses.csv"

# Function to initialize the CSV file
def initialize_file():
    try:
        with open(FILENAME, mode='x', newline='') as file:
            writer = csv.writer(file)
            writer.writerow(['Date', 'Category', 'Description', 'Amount'])
    except FileExistsError:
        pass  # File already exists, no need to create again

# Function to add an expense
def add_expense():
    category = input("Enter category (e.g., Food, Travel, Bills): ")
    description = input("Enter description: ")
    amount = float(input("Enter amount: ₹ "))
    date = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    with open(FILENAME, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([date, category, description, amount])
    
    print(" Expense added successfully!")

# Function to view all expenses
def view_expenses():
    try:
        with open(FILENAME, mode='r') as file:
            reader = csv.reader(file)
            next(reader)  # Skip header
            for row in reader:
                print(f"{row[0]} | {row[1]} | {row[2]} | ₹{row[3]}")
    except FileNotFoundError:
        print(" No expenses found yet.")

# Function to view total expenses
def view_total():
    total = 0.0
    try:
        with open(FILENAME, mode='r') as file:
            reader = csv.reader(file)
            next(reader)  # Skip header
            for row in reader:
                total += float(row[3])
        print(f" Total Expenses: ₹{total}")
    except FileNotFoundError:
        print(" No expenses to calculate total.")

# Main menu
def main():
    initialize_file()
    while True:
        print("\n===== Expense Tracker =====")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. View Total")
        print("4. Exit")
        
        choice = input("Choose an option (1-4): ")
        
        if choice == '1':
            add_expense()
        elif choice == '2':
            view_expenses()
        elif choice == '3':
            view_total()
        elif choice == '4':
            print(" Exiting... Thank you!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
#another project
