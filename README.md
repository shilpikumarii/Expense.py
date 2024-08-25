# Expense.py
import datetime

# Global list to store expense entries
expenses = []


def input_expense():
    """
    Prompts the user to enter expense details.

    Returns:
        dict: A dictionary containing the amount, category, and description of the expense.
        None: If the input is invalid.
    """
    try:
        amount = float(input("Enter the amount spent: "))
        #chose the category
        category = input("Enter the category (e.g., food, transportation, entertainment): ").strip().lower()
        description = input("Enter a brief description: ").strip()
        date = input("Enter the date (YYYY-MM-DD) of the expense: ").strip()
        date = datetime.datetime.strptime(date, "%Y-%m-%d")  # Convert string to datetime object

        return {"amount": amount, "category": category, "description": description, "date": date}
    except ValueError as e:
        print(f"Invalid input! {e}")
        return None


def add_expense(expense):
    """
    Adds an expense to the expenses list.

    Args:
        expense (dict): The expense data to add.
    """
    if expense:
        expenses.append(expense)
        print("Expense added successfully.")
    else:
        print("Expense not added due to invalid input.")


def summarize_expenses():
    """
    Summarizes expenses by category and month and displays the results.
    """
    category_totals = {}
    monthly_totals = {}

    for expense in expenses:
        category = expense['category']
        amount = expense['amount']
        date = expense['date']

        # Category-wise totals
        if category in category_totals:
            category_totals[category] += amount
        else:
            category_totals[category] = amount

        # Monthly totals (using YYYY-MM format for simplicity)
        month = date.strftime("%Y-%m")
        if month in monthly_totals:
            monthly_totals[month] += amount
        else:
            monthly_totals[month] = amount

    print("\nCategory-wise Expenditure:")
    for category, total in category_totals.items():
        print(f"{category}: ${total:.2f}")

    print("\nMonthly Expenditure:")
    for month, total in monthly_totals.items():
        print(f"{month}: ${total:.2f}")


def main():
    """
    Main function to run the Expense Tracker program.
    """
    while True:
        print("\nExpense Tracker")
        print("1. Add an Expense")
        print("2. View Summary")
        print("3. Exit")
        choice = input("Enter your choice (1/2/3): ").strip()

        if choice == '1':
            expense = input_expense()
            add_expense(expense)
        elif choice == '2':
            summarize_expenses()
        elif choice == '3':
            print("Exiting Expense Tracker. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter 1, 2, or 3.")


if __name__ == "__main__":
    main()
