# python-homework
## Background

You've made it! It's time to put away the Excel sheet and join the big leagues. Welcome to the world of programming with Python. In this homework assignment, you'll be using the concepts you've learned to complete **two** Python activities, PyBank and PyRamen. Both activities present a real-world situation in which your newfound Python skills will come in handy. These activities are far from easy, though, so expect some hard work ahead!

## Before You Begin

1. Create a new GitHub repo called `python-homework`. Then, clone it to your computer.

2. In your local git repository, create a directory for both of the Python activities. Use folder names that correspond to the activities: **PyBank** and **PyRamen**.

3. In each folder you just created, add a new file called `main.ipynb`. Remember that to create this file you will need to use JupyterLab to correctly generate the .ipynb file format. This will be the main notebook to run for each analysis.

4. Push the above changes to GitHub.

## PyBank

![Revenue](Images/revenue-per-lead.jpg)

In this activity, you are tasked with creating a Python script for analyzing the financial records of your company. You will be provided with a financial dataset in this file: [budget_data.csv](PyBank/Resources/budget_data.csv). This dataset is composed of two columns, Date and Profit/Losses. (Thankfully, your company has rather lax standards for accounting, so the records are simple.)

Your task is to create a Python script that analyzes the records to calculate each of the following:

* The total number of months included in the dataset.

* The net total amount of Profit/Losses over the entire period.

* The average of the changes in Profit/Losses over the entire period.

* The greatest increase in profits (date and amount) over the entire period.

* The greatest decrease in losses (date and amount) over the entire period.

Your resulting analysis should look similar to the following:

  ```text
  Financial Analysis
  ----------------------------
  Total Months: 86
  Total: $38382578
  Average  Change: $-2315.12
  Greatest Increase in Profits: Feb-2012 ($1926159)
  Greatest Decrease in Profits: Sep-2013 ($-2196167)
  ```

Your final script should print the analysis to the terminal and export a text file with the results.

## PyRamen (Optional)

![ramen.jpg](Images/ramen.jpg)

## Background

Welcome to Ichiban Ramen!

Opening a ramen shop has always been your dream, and now it's finally been realized––you're closing out on your second year of sales! Like last year, you need to analyze your business's financial performance by cross-referencing your sales data with your internal menu data to figure out revenues and costs for the year.

This year, you also want to analyze how well your business did on a per-product basis (as you have several choices of ramen) in order to better understand which products are doing well, which are doing poorly, and, ultimately, which products may need to be removed or changed.

You tried doing this type of per-product analysis last year in Excel, but you were not able to keep your reports up-to-date with your current sales data. Therefore, you need to innovate. With more customers and more data to process, you'll need a tool that will allow you to automate your calculations in a manner that scales with your business.

Enter Python! Python provides a wide range of capabilities for handling data, harnessing the power of low-level Python data structures and high-level development libraries, all the while supporting the automation and scalability needs for a growing enterprise.

In this homework assignment, you will need to:

1. [Read the Data](#Read-the-Data)

2. [Manipulate the Data](#Manipulate-the-Data)

---

## Instructions

### Read the Data

Complete the following:

* Read in `menu_data.csv` and set its contents to a separate list object. (This way, you can cross-reference your menu data with your sales data as you read in your sales data in the coming steps.)

  * Initialize an empty `menu` list object to hold the contents of `menu_data.csv`.

  * Use a `with` statement and open the `menu_data.csv` by using its file path.

  * Use the `reader` function from the `csv` library to begin reading `menu_data.csv`.

  * Use the `next` function to skip the header (first row of the CSV).

  * Loop over the rest of the rows and append every row to the `menu` list object (the outcome will be a list of lists).

* Set up the same process to read in `sales_data.csv`. However, instead append every row of the sales data to a new `sales` list object.

### Manipulate the Data

Complete the following:

* Initialize an empty `report` dictionary to hold the future aggregated per-product results. The `report` dictionary will eventually contain the following metrics:

  * `01-count`: the total quantity for each ramen type

  * `02-revenue`: the total revenue for each ramen type

  * `03-cogs`: the total cost of goods sold for each ramen type

  * `04-profit`: the total profit for each ramen type

* Then, loop through every row in the `sales` list object.

  * For each row of the `sales` data, set the following columns of the sales data to their own variables:

    * Quantity
    * Menu_Item

  * Perform a quick check if the `sales_item` is already included in the `report`. If not, initialize the key-value pairs for the particular `sales_item` in the report. Then, set the `sales_item` as a new key to the `report` dictionary and the values as a nested dictionary containing the following:

    ```python
    {
    "01-count": 0,
    "02-revenue": 0,
    "03-cogs": 0,
    "04-profit": 0,
    }
    ```

* Create a nested loop by looping through every record in `menu`.

  * For each row of the `menu` data, set the following columns of the menu data to their own variables:

    * Item
    * Price
    * Cost

  * If the `sales_item` in sales is equal to the `item` in `menu`, capture the `quantity` from the sales data and the `price` and `cost` from the menu data to calculate the `profit` for each item.

    * Cumulatively add the values to the corresponding metrics in the report like so:

      ```python
      report[sales_item]["01-count"] += quantity
      report[sales_item]["02-revenue"] += price * quantity
      report[sales_item]["03-cogs"] += cost * quantity
      report[sales_item]["04-profit"] += profit * quantity
      ```

  * Else print the message "{sales_item} does not equal {item}! NO MATCH!".

* Write out the contents of the `report` dictionary to a text file. The report should output each ramen type as the keys and `01-count`, `02-revenue`, `03-cogs`, and `04-profit` metrics as the values for every ramen type as shown:
