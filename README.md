# Restaurant Table Reservation App

> Mobile & Distributed Systems (CN6035)
> School of Architecture, Computing & Engineering
> Assignment Title: Development of a Restaurant Seat Reservation App via Mobile Device

##  Overview
This project is a complete mobile application that allows users to browse restaurants, make table reservations, and manage their bookings through a user-friendly interface. The system is built as a distributed architecture using **React Native (frontend)**, **Node.js/Express (backend)**, and **MariaDB (database)**.

## ⚖ Goal
To design and implement a distributed system that simulates a real-world restaurant reservation platform, integrating authentication, data management, and a responsive mobile UI.

---

##  Technologies Used
- **Frontend**: React Native (Expo)
- **Backend**: Node.js + Express
- **Database**: MariaDB
- **Authentication**: JWT (JSON Web Token)
- **Testing & API Debugging**: Postman
- **Version Control**: Git + GitHub

---

## Features
###  User Authentication
- Register with name, email, phone, birthdate & password
- Login with JWT authentication

###  Restaurant Listing
- View full list of restaurants with detailed info (location, cuisine, opening hours)
- Nice card-based UI with hover and selection effect

###  Booking Form
- Select date (date picker) and time (modal with only available slots)
- Auto-fill restaurant & user info
- Limit reservations to max 20 people (with a message for >20)
- Only future times available, up to 2 hours before closing

###  Booking History
- View past and upcoming reservations
- Edit or delete future bookings (disabled for past ones)

###  Profile
- Welcome message & logout button
- Session management using AsyncStorage

###  UI Design
- Modern lilac styling
- Modal confirmations
- Bottom tab bar navigation (Restaurants / History / Profile)

---

##  Installation Instructions
### Prerequisites
- Node.js
- npm or yarn
- MariaDB
- Expo CLI (`npm install -g expo-cli`)

### 1. Backend Setup
```bash
cd backend
npm install
```

#### Environment File (.env)
```
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=yourpassword
DB_DATABASE=restaurant_booking
JWT_SECRET=mysecretjwt
PORT=5001
```

#### Start Backend Server
```bash
node server.js
```

### 2. Database Setup (MariaDB)
```sql
CREATE DATABASE restaurant_booking;

CREATE TABLE users (
  user_id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255),
  email VARCHAR(255),
  phone VARCHAR(20),
  birthdate DATE,
  password VARCHAR(255)
);

CREATE TABLE restaurants (
  restaurant_id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(255),
  location VARCHAR(255),
  opening_time TIME,
  closing_time TIME
);

CREATE TABLE reservations (
  reservation_id INT PRIMARY KEY AUTO_INCREMENT,
  user_id INT,
  restaurant_id INT,
  date DATE,
  time TIME,
  people_count INT,
  comments TEXT,
  FOREIGN KEY (user_id) REFERENCES users(user_id),
  FOREIGN KEY (restaurant_id) REFERENCES restaurants(restaurant_id)
);
```

### 3. Frontend Setup
```bash
cd frontend
npm install
npx expo start
```

---

##  Screenshots

###  Login Screen
![Login Screen](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2017.53.35.png)

User enters email and password to authenticate. Error messages are shown for invalid credentials. 

###  Signup Screen
![Signup Screen](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2017.53.39.png)

User registers with full name, email, phone, birth date, and password. Password validation requires at least one uppercase letter and one number.

###  Restaurants List
![Restaurants List](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2017.54.09.png)

Displays all available restaurants with cards showing name, location, phone, cuisine type, and opening hours.

###  Booking Screen
![Booking Screen](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2017.54.15.png)

Reservation form where user selects the restaurant, date (using date picker), time (using modal with available slots), number of people, and optional comments.

###  Time Picker (Booking)
![Time Picker Booking](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2018.08.48.png)

Only available times are shown based on the restaurant’s opening/closing times. Past times and late-night bookings are excluded.

###  Booking Confirmation
![Booking Confirmation](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2018.27.32.png)

Displays a success message after a booking is submitted. Confirms the restaurant name, date, time, number of people, and any comments.

###  Reservations History
![Reservations History](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2018.09.28.png)

Lists the user's current and past reservations. Future reservations include options to edit or delete. Past reservations are read-only.

###  Edit Reservation
![Edit Reservation](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2018.27.41.png)

Form allowing user to update an existing reservation (date, time, people count, comments). Includes availability check for new times.

###  Update Confirmation
![Update Confirmation](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2018.28.03.png)

After editing a reservation, a success message is displayed confirming the update.

###  Profile Screen
![Profile Screen](assets/screenshots/Simulator%20Screenshot%20-%20iPhone%2016%20Plus%20-%202025-04-25%20at%2018.09.43.png)
Profile page showing a welcome message with the user's name and a logout button to safely exit the session.


---

##  Authentication Flow
- Passwords are hashed using bcrypt
- JWT token is returned on login and stored in AsyncStorage
- Token is required for all reservation endpoints

---

## API Endpoints
### Auth
- `POST /register`
- `POST /login`

### Restaurants
- `GET /restaurants`

### Reservations
- `POST /reservations`
- `GET /reservations/available`
- `GET /users/me`
- `PUT /reservations/:id`
- `DELETE /reservations/:id`

---

##  Usage Example
```bash
1. Register new user
2. Login -> get JWT
3. Fetch restaurants -> choose one
4. Select date, time, number of people
5. Confirm booking
6. View & manage bookings in History
```

---

##  Project Highlights
- End-to-end functional app with modern UI
- Real-time validation and dynamic availability
- Separation of concerns: UI / API / DB
- Compliant with all assignment requirements (CN6035)

---

##  Credits
Developed by Aimilia Michali
University of East London (CN6035)

---

##  GitHub Repository
[https://github.com/emilymixali/restaurant-reservation-app-CN6035](https://github.com/emilymixali/restaurant-reservation-app-CN6035)

---


