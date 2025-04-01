# e-Tracker-application-over-a-7-day-period
import json
import os
from datetime import datetime
from collections import defaultdict

class ExpenseTracker:
    def __init__(self):
        self.expenses = []
        self.categories = {
            '1': 'Food',
            '2': 'Transportation',
            '3': 'Entertainment',
            '4': 'Utilities',
            '5': 'Shopping',
            '6': 'Other'
        }
        self.data_file = 'expenses.json'
        self.load_expenses()

    def load_expenses(self):
        """Load expenses from JSON file"""
        if os.path.exists(self.data_file):
            with open(self.data_file, 'r') as file:
                try:
                    self.expenses = json.load(file)
                except json.JSONDecodeError:
                    print("Warning: Expense data file is corrupted. Starting with empty list.")
                    self.expenses = []

    def save_expenses(self):
        """Save expenses to JSON file"""
        with open(self.data_file, 'w') as file:
            json.dump(self.expenses, file, indent=4)

    def add_expense(self):
        """Add a new expense to the tracker"""
        print("\n--- Add New Expense ---")
        
        while True:
            try:
                amount = float(input("Enter amount spent: $"))
                if amount <= 0:
                    print("Amount must be positive. Please try again.")
                    continue
                break
            except ValueError:
                print("Invalid amount.
