**Movie Ticket Booking System**
**Overview**
This is a simple Movie Ticket Booking System built using Python and MySQL. The system allows users to register, log in, and book tickets for available movies. Admin users can add new movies and view all bookings.

**Features**
User Registration and Login
Role-based access (Admin/User)
Add Movies (Admin)
View Movies and Available Seats
Book Tickets
View Booking History (User)
View All Bookings (Admin)
Secure password storage using SHA-256 encryption
**Setup Instructions**
**Prerequisites**
Python 3.x
MySQL Server
MySQL Connector for Python

**Step 1: Install Required Libraries**
To install the required Python libraries, use the following command:
pip install mysql-connector-python
**Step 2: Set Up the MySQL Database**
Create a MySQL database named movie_ticket_online.
Run the following SQL queries to set up the required tables:

CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('user', 'admin') NOT NULL
);

CREATE TABLE Movies (
    movie_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    showtime DATETIME NOT NULL,
    price DECIMAL(10, 2) NOT NULL
);

CREATE TABLE Seats (
    seat_id INT AUTO_INCREMENT PRIMARY KEY,
    movie_id INT NOT NULL,
    seat_number INT NOT NULL,
    is_booked BOOLEAN DEFAULT 0,
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id)
);

CREATE TABLE Bookings (
    booking_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    movie_id INT NOT NULL,
    seat_id INT NOT NULL,
    booking_time DATETIME NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (movie_id) REFERENCES Movies(movie_id),
    FOREIGN KEY (seat_id) REFERENCES Seats(seat_id)
);

**Step 3: Configure Database Connection**
In the main.py file, update the MySQL connection details in the create_connection function:

connection = mysql.connector.connect(
    host="localhost",
    user="your_mysql_username",
    password="your_mysql_password",
    database="movie_ticket_online"
)

**Step 4: Running the Application**
Ensure the MySQL server is running.
Run the Python script using:
python main.py

Usage
Once the program is running:
**Register a user:**
Users can register by entering a username, password, and role (admin/user).
**Login:**
Users can log in to access the system features.
**Admin Functions:**
Add new movies to the system.
View all booking details.
**User Functions:**
View available movies.
Book seats for a selected movie.
View booking history.
**Security**
Passwords are securely hashed using SHA-256 before being stored in the database.
**Future Improvements**
Add functionality for canceling bookings.
Enhance seat selection with a visual interface.
Implement email or SMS notifications for bookings.
