# Homework02
Homework02

import pandas as pd

def main():

    

    #: Open "Budget_data.csv" file with Pandas
    budget_df = pd.read_csv('budget_data.csv')

    #  Profit info
    budget_info = budget_df['Profit/Losses'].describe()

    count = int(budget_info['count'])
    total_net = budget_df['Profit/Losses'].sum()

    # Each column for Date and Profit
    profit_series = budget_df['Profit/Losses']
    date_series = budget_df['Date']

    total_changes = 0
    great_increase = 0
    great_decrease = 0

    great_increase_date = date_series[0]
    great_decrease_date = date_series[0]

    #Get the Total Change, Greate Increase, Greate Decrease
    for index in range(count - 1):
        change = profit_series[index + 1] - profit_series[index]
        #! Get Greate Incrase
        if change > great_increase:
            great_increase = change
            great_increase_date = date_series[index]

        #! Get Greate Increase
        if change < great_decrease:
            great_decrease = change
            great_decrease_date = date_series[index]

        #! Get Total Changes
        total_changes += (profit_series[index + 1] - profit_series[index])

    average_change = total_changes / (count - 1)
    
    print("Financial Analysis")
    print("-----------------------------")

    print("Total Month: " + str(count))    
    print("Total: $" + str(total_net))
    print("Average Change: $" + str(average_change))
    print("Greatest Increase in Profit: " + great_increase_date + " ($" + str(great_increase) + ")")
    print("Greatest Decrease in Profit: " + great_decrease_date + " ($" + str(great_decrease) + ")")
    

main()
