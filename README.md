# Restaurant in Anchorage Data Analysis Project

This repository contains a data analysis project focused on a fictional restaurant in Anchorage, specializing in pizza and other dishes. The project demonstrates the end-to-end process of **database creation, querying, and dashboard reporting** using:

- **MySQL 8.0**  
- **MySQL Workbench** and **Navicat** for local development and management  
- **Google Cloud MySQL** for deployment  
- **Looker Studio** (formerly Google Data Studio) for dashboards and reporting  

All data in the database tables was **generated by ChatGPT**.  

---

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Database Design](#database-design)  
3. [Queries](#queries)  
4. [Dashboards and Reports](#dashboards-and-reports)  
5. [Tech Stack](#tech-stack)  
6. [How to Use](#how-to-use)  
7. [Future Enhancements](#future-enhancements)  

---

## Project Overview

The primary goal of this project is to **analyze restaurant data** for better decision-making. We focus on:
- Orders (which items are most popular, how many items per order, etc.)  
- Inventory and Ingredients (ingredient costs, remaining stock)  
- Staff shifts and costs  

By combining **structured queries** with **dynamic dashboards**, we gain insights into:
- Total orders and sales  
- Average order value  
- Most popular dishes, pizzas, or ingredients  
- Delivery vs. dine-in trends  
- Staff costs and hours  

---

## Database Design

The database schema was initially drafted with **[QuickDBD](https://www.quickdatabasediagrams.com/)**, resulting in the following tables:

1. **Orders**  
   - **Fields**: row_id, order_id, created_at, item_id, quantity, cust_id, delivery, add_id  
   - Tracks each order’s timestamp, ordered items, and related customer info.

2. **Customers**  
   - **Fields**: cust_id, cust_firstname, cust_lastname  
   - Stores basic information for each customer.

3. **Address**  
   - **Fields**: add_id, delivery_address1, delivery_address2, delivery_city, delivery_zipcode  
   - Holds delivery addresses for orders.

4. **Item**  
   - **Fields**: item_id, sku, item_name, item_cat, item_size, item_price  
   - Catalog of menu items, including category (e.g., pizza, side, drink), size, and price.

5. **Ingredient**  
   - **Fields**: ing_id, ing_name, ing_weight, ing_meas, ing_price  
   - Contains all ingredients used in menu items, their weight, measure type, and cost.

6. **Recipe**  
   - **Fields**: row_id, recipe_id, ing_id, quantity  
   - Defines which ingredients go into each recipe (item).

7. **Inventory**  
   - **Fields**: inv_id, item_id, quantity  
   - Tracks the stock levels of each item or ingredient.

8. **Staff**  
   - **Fields**: staff_id, first_name, last_name, position, hourly_rate  
   - Stores details about restaurant staff, including their hourly pay.

9. **Rota**  
   - **Fields**: row_id, rota_id, date, shift_id, staff_id  
   - Schedules staff for shifts on given dates.

10. **Shift**  
    - **Fields**: shift_id, day_of_week, start_time, end_time  
    - Defines shifts, including the day of the week and time interval.

**Diagram Documentation** (from QuickDBD export) is included in the [diagram documentation section](#) of this README (or in a separate `.png`/`.pdf` file if you uploaded it).

---

## Queries

Four main queries were crafted to analyze the data:

1. **`select_orders_join.sql`**  
   - Demonstrates how to join the `Orders`, `Item`, `Customers`, and `Address` tables.  
   - Used for calculating total orders, total items sold, and average order size.

2. **`ingredient_cost_query.sql`**  
   - Joins `Ingredient` and `Recipe` tables to determine the cost of each ingredient used in menu items.  
   - Helps find the *most expensive* and *most commonly used* ingredients.

3. **`remaining_weight_query.sql`**  
   - Checks the `Inventory` table to see how much of each ingredient remains.  
   - Useful for **stock-level monitoring** and ordering decisions.

4. **`staff_cost_query.sql`**  
   - Calculates total staff cost based on `Rota`, `Shift`, and `Staff` tables.  
   - Evaluates hours worked, hourly rates, and total cost per date range.

---

## Dashboards and Reports

### Looker Studio Dashboards

After uploading the MySQL data to **Google Cloud MySQL**, we utilized **Looker Studio** to create dynamic dashboards:

- **Order Metrics**: 
  - Total orders, total sales, total items sold, and **average order value**.  
  - Graphical breakdown of the most popular dishes (especially pizza flavors/types).

- **Delivery vs. Dine-In**: 
  - Compares how many orders are for delivery versus dine-in, providing insights on logistics.

- **Location Insights**: 
  - City or ZIP-based breakdown to see where orders come from.

- **Ingredient Management**: 
  - Highlights ingredient costs, most popular ingredients, remaining ingredients in the warehouse.  
  - Color-coded signals (green/yellow) to indicate items that need restocking.

- **Staffing and Costs**: 
  - Shows staff schedules and total hours worked in a selected date range.  
  - Displays total staff cost, positions, hourly rates, and individual contributions to labor expenses.

These dashboards allow managers to make **faster, data-driven decisions** regarding menu popularity, inventory restocking, and staffing needs.

---

## Tech Stack

- **MySQL 8.0**  
- **MySQL Workbench** & **Navicat** for local DB management  
- **QuickDBD** for initial database diagramming  
- **Google Cloud MySQL** hosting for final data store  
- **Looker Studio** for interactive dashboards  
- **ChatGPT** for synthetic data generation  

---

## How to Use

1. **Clone or Download** this repository.  
2. **Create the Database**:  
   - Use the provided `.sql` file to create the schema and populate the tables.  
   - Alternatively, import the schema from the QuickDBD export.  
3. **Run Queries**:  
   - Execute `Project1.sql`,`select_orders_join.sql`, `ingredient_cost_query.sql`, `remaining_weight_query.sql`, and `staff_cost_query.sql` to see the sample results.  
4. **View Dashboards**:  
   - If you have access to Looker Studio with the connected Google Cloud MySQL, open the provided Looker Studio reports, or replicate them based on the SQL queries.  

---

## Future Enhancements

- **Add More Dimensions**: Expand tables for marketing campaigns or customer feedback to analyze seasonal promotions.  
- **Real-Time Dashboard**: Integrate streaming data from the restaurant’s POS system for real-time insights.  
- **Machine Learning**: Predict popular menu items and forecast ingredient usage.  
- **Automated Alerts**: Set up triggers in MySQL or Looker Studio to alert managers when certain inventory levels fall below a threshold.  

---

**Thank you for checking out this project!** Feel free to explore, fork, and submit pull requests with improvements or suggestions. If you have any questions, create an issue or contact the project maintainer.
