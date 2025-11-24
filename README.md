# cse1024[cse project.py](https://github.com/user-attachments/files/23707336/cse.project.py)

import mysql.connector

# --- 1. Establish a Database Connection ---

try:
    connection = mysql.connector.connect(host="localhost",user="root",Passwd="sabitabhatt",database="mylibrary")
return connection
except mysql.connector.Error as err:
    print(f"Error connecting to MySQL: {err}")
return None

# --- 2. Example Function: Add a Book ---
def add_book():
    bookname=input("Enter the name of the book = ")
    writer=input("Enter the name of the writer = ")
    quantity=int(input("Enter the quantity of books = "))
    connection = create_connection()
    if connection:
        cursor = connection.cursor()
        sql_query = "INSERT INTO books VALUES (bookname,writer, quantity)"
        data = (bookname,writer,quantity)
        try:
            cursor.execute(sql_query, data)
            connection.commit() # Essential to save changes
            print("Book added successfully!")
        except mysql.connector.Error as err:
            print(f"Error adding book: {err}")
        finally:
            cursor.close()
            connection.close()

# --- 3. Example Function: View All Books ---
def view_books():
    connection = create_connection()
    if connection:
        cursor = connection.cursor()
        sql_query = "SELECT * FROM books"
        try:
            cursor.execute(sql_query)
            results = cursor.fetchall()
            if results:
                print("Library Books:")
                for row in results:
                    print(f"Code: {row[2]}, Title: {row[0]}, Author: {row[1]}, Total Copies: {row[3]}")
            else:
                print("No books found.")
        except mysql.connector.Error as err:
            print(f"Error viewing books: {err}")
        finally:
            cursor.close()
            connection.close()
add_book()
view_book()

