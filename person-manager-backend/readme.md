# Person Manager Backend

This is the backend API for the Person Manager application, built with Node.js, Express, and MongoDB.

## Prerequisites

- Node.js (version 14 or higher)
- MongoDB (local installation or cloud service like MongoDB Atlas)
- npm or yarn

## Installation

1. Clone the repository:
   ```
   git clone <repository-url>
   cd person-manager-backend
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Create a `.env` file in the root directory and add your environment variables:
   ```
   PORT=5000
   MONGODB_URI=mongodb://localhost:27017/person-manager
   # Or for MongoDB Atlas: MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/person-manager
   ```

## Running the Application

### Development Mode
```
npm run dev
```
This will start the server with nodemon for automatic restarts on file changes.

### Production Mode
```
npm start
```
This will start the server with Node.js.

The server will run on `http://localhost:5000` by default (or the port specified in your `.env` file).

## API Endpoints

- `GET /api/persons` - Get all persons
- `POST /api/persons` - Create a new person
- `GET /api/persons/:id` - Get a person by ID
- `PUT /api/persons/:id` - Update a person by ID
- `DELETE /api/persons/:id` - Delete a person by ID

## Project Structure

- `server.js` - Main server file
- `models/Person.js` - Person model
- `routes/personRoutes.js` - API routes for persons
- `.env` - Environment variables (not committed to version control)

## Technologies Used

- Express.js - Web framework
- MongoDB - Database
- Mongoose - ODM for MongoDB
- CORS - Cross-origin resource sharing
- Morgan - HTTP request logger
- Dotenv - Environment variable management
