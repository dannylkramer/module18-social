# Social Network API

## Description
This is a social network web application API where users can share their thoughts, react to friends' thoughts, and create a friend list. The API uses Express.js for routing, a MongoDB database, and the Mongoose ODM.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Models](#models)
- [API Routes](#api-routes)
- [Testing](#testing)
- [License](#license)
- [Questions](#questions)

## Installation
1. Clone the repository:
    ```bash
    git clone https://github.com/your-username/social-network-api.git
    ```
2. Navigate to the project directory:
    ```bash
    cd social-network-api
    ```
3. Install the dependencies:
    ```bash
    npm install
    ```

## Usage
1. Ensure MongoDB is running on your machine. If not, you can start it with:
    ```bash
    mongod
    ```
2. Start the application:
    ```bash
    npm start
    ```
   If you want to use `nodemon` for development, you can use:
    ```bash
    npx nodemon server.js
    ```

## Models
### User Model
- **username**: String, unique, required, trimmed
- **email**: String, required, unique, must match a valid email address
- **thoughts**: Array of `_id` values referencing the Thought model
- **friends**: Array of `_id` values referencing the User model (self-reference)
- **Virtuals**: `friendCount` retrieves the length of the user's friends array field

### Thought Model
- **thoughtText**: String, required, must be between 1 and 280 characters
- **createdAt**: Date, default value to the current timestamp, formatted on query
- **username**: String, required
- **reactions**: Array of nested documents created with the reactionSchema
- **Virtuals**: `reactionCount` retrieves the length of the thought's reactions array field

### Reaction Schema (Subdocument of Thought)
- **reactionId**: ObjectId, default value set to a new ObjectId
- **reactionBody**: String, required, 280 character maximum
- **username**: String, required
- **createdAt**: Date, default value to the current timestamp, formatted on query

## API Routes
### Users
- **GET /api/users**: Get all users
- **GET /api/users/:userId**: Get a single user by its `_id` and populated thought and friend data
- **POST /api/users**: Create a new user
- **PUT /api/users/:userId**: Update a user by its `_id`
- **DELETE /api/users/:userId**: Remove user by its `_id`
- **BONUS**: Remove a user's associated thoughts when deleted

### Friends
- **POST /api/users/:userId/friends/:friendId**: Add a new friend to a user's friend list
- **DELETE /api/users/:userId/friends/:friendId**: Remove a friend from a user's friend list

### Thoughts
- **GET /api/thoughts**: Get all thoughts
- **GET /api/thoughts/:thoughtId**: Get a single thought by its `_id`
- **POST /api/thoughts**: Create a new thought and push the created thought's `_id` to the associated user's thoughts array field
- **PUT /api/thoughts/:thoughtId**: Update a thought by its `_id`
- **DELETE /api/thoughts/:thoughtId**: Remove a thought by its `_id`

### Reactions
- **POST /api/thoughts/:thoughtId/reactions**: Create a reaction stored in a single thought's reactions array field
- **DELETE /api/thoughts/:thoughtId/reactions/:reactionId**: Remove a reaction by the reaction's reactionId value

## Testing
To test the application, you can use tools like Insomnia, Postman, or cURL to make HTTP requests to the API endpoints. Here are some example requests you can try:

### Users
- **Create a User**:
  - Method: POST
  - URL: `/api/users`
  - Body:
    ```json
    {
      "username": "lernantino",
      "email": "lernantino@gmail.com"
    }
    ```

- **Get All Users**:
  - Method: GET
  - URL: `/api/users`

- **Get a User by ID**:
  - Method: GET
  - URL: `/api/users/:userId`

### Thoughts
- **Create a Thought**:
  - Method: POST
  - URL: `/api/thoughts`
  - Body:
    ```json
    {
      "thoughtText": "Here's a cool thought...",
      "username": "lernantino",
      "userId": "5edff358a0fcb779aa7b118b"
    }
    ```

- **Get All Thoughts**:
  - Method: GET
  - URL: `/api/thoughts`

- **Get a Thought by ID**:
  - Method: GET
  - URL: `/api/thoughts/:thoughtId`

## License
This project is licensed under the MIT License.

## Questions
If you have any questions about the project, please open an issue or contact me directly at [your-email@example.com](mailto:your-email@example.com). You can find more of my work on my [GitHub profile](https://github.com/your-username).
