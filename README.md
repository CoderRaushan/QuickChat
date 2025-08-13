# QuickChat

QuickChat is a full-stack social media and chat application featuring real-time messaging, stories, posts, comments, notifications, and more. The project is split into two main parts:

- [`QuickChatBackend`](https://github.com/CoderRaushan/QuickChatBackend) – Node.js/Express backend with MongoDB, REST APIs, authentication, and real-time socket communication.
- [`QuickChatFrontend`](https://github.com/CoderRaushan/QuickChatFrontend) – React frontend with Redux, Vite, and Tailwind CSS.

---

## Features

### User Authentication
- Email/password signup with email verification
- Social login (Google, GitHub, YouTube, LinkedIn)
- JWT-based authentication and session management

### Profile & Social Graph
- User profile with avatar, bio, website, and more
- Edit profile, change avatar
- Follow/unfollow users
- Suggested users

### Posts & Comments
- Create, view, like, dislike, bookmark, and delete posts
- Upload images, videos, audio, PDFs, and documents
- Comment on posts, view all comments

### Stories
- Create and view stories (image/video, 24h expiry)
- See stories from users you follow
- Like and view count for stories

### Messaging
- Real-time 1:1 chat with text and file sharing (images, videos, audio, PDFs, docs)
- Typing indicators
- Message status (sent, delivered, seen)
- Infinite scroll for chat history

### Notifications
- Real-time notifications for likes, comments, follows, and messages

## Tech Stack

### Backend
- Node.js, Express.js
- MongoDB & Mongoose
- Socket.io for real-time messaging
- AWS S3 for file uploads (presigned URLs)
- Passport.js for OAuth (Google, GitHub, LinkedIn, YouTube)
- Nodemailer for email verification and welcome emails
- Cloudinary for image uploads
- JWT for authentication

### Frontend
- React (with Vite)
- Redux Toolkit for state management
- React Router for navigation
- Tailwind CSS for styling
- Axios for API requests
- React Toastify for notifications
- Masonry layout for posts
- File upload and preview
- Responsive design

---

## Folder Structure

```
QuickChat/
│
├── QuickChatBackend/
│   ├── app.js
│   ├── Dockerfile
│   ├── package.json
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middlewares/
│   ├── socket/
│   ├── utils/
│   └── CloudConfig/
│
├── QuickChatFrontend/
│   ├── src/
│   │   ├── components/
│   │   ├── ReduxStore/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── ...
│   ├── public/
│   ├── Dockerfile
│   ├── package.json
│   ├── tailwind.config.js
│   └── ...
│
├── docker-compose.yml
└── README.md
```

---

## Getting Started

### Prerequisites

- Node.js (v16+)
- MongoDB instance (local or cloud)
- AWS S3 bucket (for file uploads)
- Cloudinary account (for images)
- SMTP credentials (for email)
- (Optional) Docker

### Environment Variables

#### Backend (`QuickChatBackend/.env`)
```
MONGODB_URI=your_mongodb_uri
JWT_SECRET=your_jwt_secret
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
AWS_REGION=your_aws_region
AWS_S3_BUCKET=your_bucket
CLOUDINARY_CLOUD_NAME=your_cloudinary_name
CLOUDINARY_API_KEY=your_cloudinary_key
CLOUDINARY_API_SECRET=your_cloudinary_secret
QUICK_CHAT_EMAIL_ADDRESSS=your_email@example.com
SMTP_PASS=your_email_password
CLIENT_URL=http://localhost:5173
```

#### Frontend (`QuickChatFrontend/.env`)
```
VITE_MainUri=http://localhost:4234
```

---

## Installation

### 1. Clone the repository

```sh
git clone https://github.com/CoderRaushan/QuickChat
cd QuickChat
```

### 2. Setup Backend

```sh
cd QuickChatBackend
npm install
# Set up your .env file as described above
npm start
```

### 3. Setup Frontend

```sh
cd ../QuickChatFrontend
npm install
# Set up your .env file as described above
npm run dev
```

### 4. (Optional) Run with Docker

```sh
docker-compose up --build
```

---

## Usage

- Visit `http://localhost:5173` to access the frontend.
- Register a new account or sign in with social providers.
- Create posts, upload files, comment, like, and bookmark.
- Start chats with other users, send messages and files in real-time.
- View and create stories.
- Edit your profile and follow/unfollow users.

---

## API Endpoints

### Auth & User
- `POST /auth/signup` – Register
- `POST /auth/signin` – Login
- `POST /auth/verify-email` – Email verification
- `GET /user/:id/profile` – Get user profile
- `PUT /user/edit/profile` – Edit profile
- `POST /user/followOrUnfollow/:id` – Follow/unfollow

### Posts
- `POST /user/post/add` – Create post
- `GET /user/post/all` – Get all posts
- `POST /user/post/:id/comment` – Add comment
- `GET /user/post/:id/comment/all` – Get comments
- `GET /user/post/:id/like` – Like post
- `GET /user/post/:id/dislike` – Dislike post
- `POST /user/post/:id/bookmark` – Bookmark post
- `DELETE /user/post/delete/:id` – Delete post

### User (Follow/Unfollow)
- `POST /user/followOrUnfollow/:id` – Follow or unfollow a user
- `GET /user/followers/:id` – Get followers of a user
- `GET /user/followings/:id` – Get users followed by a user

### Post (Like, Dislike, Comment, Bookmark)
- `POST /user/post/add` – Create a new post
- `GET /user/post/all` – Get all posts
- `GET /user/post/:id` – Get a single post by ID
- `GET /user/post/:id/like` – Like a post
- `GET /user/post/:id/dislike` – Dislike a post
- `POST /user/post/:id/comment` – Add a comment to a post
- `GET /user/post/:id/comment/all` – Get all comments for a post
- `POST /user/post/:id/bookmark` – Bookmark a post
- `DELETE /user/post/delete/:id` – Delete a post

### Comment (Like/Dislike)
- `POST /user/comment/:id/like` – Like a comment
- `POST /user/comment/:id/dislike` – Dislike a comment

### Story (Like, View)
- `POST /user/story/likeAndDislike/:storyId` – Like or dislike a story
- `POST /user/story/view/:storyId` – Mark a story as viewed

### Stories
- `POST /user/story/upload` – Upload story
- `GET /user/story/:userId` – Get user stories
- `POST /user/story/following/stories` – Get stories from followings
- `POST /user/story/view/:storyId` – View a story
- `POST /user/story/likeAndDislike/:storyId` – Like/dislike a story

### Messaging
- `POST /user/message/conversations/bulk-start` – Start conversations
- `GET /user/message/:conversationId` – Get messages for a conversation
- `POST /user/message/get-upload-url` – Get S3 presigned URL for file upload

---

## Real-Time Features

- Socket.io is used for real-time messaging, typing indicators, and notifications.
- Message delivery and seen status are updated live.
- Notifications for likes, comments, and follows are pushed instantly.

---

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Create a new Pull Request

---

## Credits

- [React](https://react.dev/)
- [Vite](https://vitejs.dev/)
- [Redux Toolkit](https://redux-toolkit.js.org/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Node.js](https://nodejs.org/)
- [Express](https://expressjs.com/)
- [MongoDB](https://www.mongodb.com/)
- [Socket.io](https://socket.io/)
- [AWS S3](https://aws.amazon.com/s3/)
- [Cloudinary](https://cloudinary.com/)
- [Passport.js](http://www.passportjs.org/)
- [Nodemailer](https://nodemailer.com/)

---

## Screenshots
### Signup
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/signup.png)

### Signin
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/signin.png)

### Home Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/Homepage.png)

### Comment Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/comments.png)

### Search Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/search.png)

### Explore Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/explore.png)

### Chat Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/message.png)

### Real-Time Notification
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/notification.png)

### Create Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/create.png)

### Profile Page
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/profile.png)

### Create Story 
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/039206d7b4f9c10d5eb18c0917a938be53aea45e/public/story1.png)

### Story Section
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/story5.png)

### Show Story 
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/story3.png)

### show Story with views & likes
![Home Page](https://github.com/CoderRaushan/QuickChatFrontend/blob/e335a641f18aca9a6d906550dda0b2d1e5df9158/public/story4.png)

## Getting Started

### Prerequisites

- **Node.js** (v16 or higher)
- **npm** (comes with Node.js)
- **MongoDB** (local or cloud instance)
- **Cloudinary** and **AWS S3** accounts (for media uploads)
- **SMTP credentials** (for email features)
- (Optional) **Docker** for containerized setup

---

### 1. Clone the Repository

```sh
git clone https://github.com/coderraushan/QuickChat
cd QuickChat
```

---

### 2. Setup the Backend

```sh
cd QuickChatBackend
npm install
```

- Create a `.env` file in `QuickChatBackend` and add the following (replace with your values):

    ```
    MONGODB_URI=your_mongodb_uri
    JWT_SECRET=your_jwt_secret
    AWS_ACCESS_KEY_ID=your_aws_access_key
    AWS_SECRET_ACCESS_KEY=your_aws_secret
    AWS_REGION=your_aws_region
    AWS_S3_BUCKET=your_bucket
    CLOUDINARY_CLOUD_NAME=your_cloudinary_name
    CLOUDINARY_API_KEY=your_cloudinary_key
    CLOUDINARY_API_SECRET=your_cloudinary_secret
    QUICK_CHAT_EMAIL_ADDRESSS=your_email@example.com
    SMTP_PASS=your_email_password
    CLIENT_URL=http://localhost:5173
    ```

- Start the backend server:

    ```sh
    npm start
    ```

---

### 3. Setup the Frontend

```sh
cd ../QuickChatFrontend
npm install
```

- Create a `.env` file in `QuickChatFrontend` and add:

    ```
    VITE_MainUri=http://localhost:4234
    ```

- Start the frontend server:

    ```sh
    npm run dev
    ```

---

### 4. Access the Application

- Open your browser and go to: [http://localhost:5173](http://localhost:5173)

---

### 5. (Optional) Docker Setup

If you want to run both backend and frontend using Docker:

```sh
docker-compose up --build
```

---

### 6. Usage

- Register a new account or sign in with social providers.
- Create posts, upload files, comment, like, and bookmark.
- Start chats with other users, send messages and files in real-time.
- View and create stories.
- Edit your profile and follow/unfollow users.

---

**Note:**  
Make sure your MongoDB, Cloudinary, AWS S3, and SMTP credentials are correct for all features to

## Contact

For questions or support, please open an issue or contact the maintainer.
