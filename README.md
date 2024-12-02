# Telegram Bot for Product Management

This project is a Telegram bot designed for managing products and orders. It allows users to interact either as **clients** or **administrators**, supporting functionalities like viewing products, making purchases, and managing product details.

## Features

### For Clients:
- View available products.
- Search for products by name or ID.
- Make purchases using Telegram Payments.

### For Administrators:
- Add new products.
- View and manage existing products.
- Create, modify product details (name, description, price), and delete products.

---

## Tech Stack
- **Python**: Core programming language for building the bot and server-side logic.
- **Aiogram**: Provides asynchronous support for handling Telegram API interactions.
- **SQLAlchemy**: Object-Relational Mapping (ORM) library for working with the database.

---

## Project Structure

### **`main.py`**
- The main entry point of the bot.
- Imports handlers and starts them using the `executor.start_polling` function.
- Sets up the database connection.

### **`bot_init.py`**
- Responsible for initializing the bot.
- Loads the bot token from the `.env` file.
- Configures the `Dispatcher` with `MemoryStorage` for managing user states.

### **`session.py`**
- A module for interacting with the database.
- Uses SQLAlchemy to create sessions and connect to PostgreSQL.
- Automatically creates the database if it doesn’t exist.

### **`models.py`**
- Contains ORM models for the database:
  - **`User`**: Stores user information.
  - **`Product`**: Describes products (name, description, price, etc.).
  - **`Order`**: Represents orders (linking users with products).
- All models interact with each other using SQLAlchemy relationships.

### **`handlers/`**
- A directory containing the main handlers for different functionalities:
  - **`addProduct.py`**: Adds new products to the database.
  - **`deleteProduct.py`**: Deletes products (marks `isSelling` as `False`).
  - **`changeProduct.py`**: Edits product information.
  - **`seeAllProducts.py`**: Displays available products.
  - **`buyProduct.py`**: Handles the product purchase process for clients.
- Each handler implements a specific bot functionality.

### **`ResponseGenerator.py`**
- Provides functions to create textual responses, such as displaying product lists or action results (e.g., purchase or deletion).

### **`state.py`**
- Configures the FSM (Finite State Machine) for tracking user states.
- Defines all the states required for processes like adding a product, making a purchase, etc.

### **`kb.py`**
- Contains keyboard definitions:
  - Inline keyboards for administrators (adding, editing, deleting products).
  - Keyboards for clients (viewing products, making purchases).

### **`updateLastMessageID.py`**
- Functions for storing the ID of the last user message.
- Enables proper keyboard updates without sending new messages.

---
# Installation
## 1. Clone the Repository
git clone https://github.com/erisfelixx/tg-bot-shop

## 2. Install Dependencies
pip install -r ./requirements.txt

## 3. Add Database Credentials to .env File
bot_token = "yourbottoken"
payment_token = "yourpaymenttoken"

user = "youruser"
psw = "yourpsw"
host = "yourhost"
port = "yourport"
db = "yourdbname"

## 4. Run the Bot
python main.py
