# Safespace

Safespace is a community platform focused on mental health discussions, built with a toxicity filter powered by machine learning. Users can create posts, reply to others, and engage in conversations while ensuring harmful content is filtered out in real time.

---

## Features

Safespace provides a safe and structured environment for users to share and support each other:

- User authentication and profile creation  
- Post creation and threaded comments  
- Real-time toxicity detection for all content  
- Automatic filtering of harmful, threatening, or hateful language  
- Secure handling of data with Firebase  

At the core of Safespace is a **TensorFlow.js toxicity detection model** that runs directly in the browser. This means every message is checked locally in real time, without needing to send content to an external server for classification. It's a lightweight but powerful way to keep the community safe while keeping the experience fast and private. The model is built on the Universal Sentence Encoder and trained on millions of labeled comments, giving it strong accuracy across a wide range of harmful language.  

---

## Architecture Overview

The project is structured with a **React frontend** and a **Firebase backend**. A TensorFlow.js model runs client-side to classify toxic content in user submissions before it is displayed.  

The frontend is implemented entirely in **React**, using **Material UI** for components and styling. Posts and comments are structured as reusable components that communicate with Firebase for persistence.  

The backend uses **Firebase Authentication** for secure sign-up and login, along with **Firestore** for storing user data and posts. **Firebase Functions** provide serverless logic for extending functionality and handling secure operations.  

The toxicity detection system is a **TensorFlow.js model** trained on the Civil Comments dataset (~2M labeled comments) and built on top of the Universal Sentence Encoder. Predictions flag content that contains:
- Threatening language
- Insults
- Obscenities
- Identity-based hate
- Sexually explicit content

---

## Tech Stack

- **Frontend**: React, Material UI  
- **Backend**: Firebase (Auth, Firestore, Functions)  
- **Machine Learning**: TensorFlow.js, Universal Sentence Encoder, Civil Comments dataset  
- **Hosting/Deployment**: Firebase Hosting  

---

## Repository Structure

```plaintext
Safespace/
├── public/                   # Static assets
├── src/
│   ├── components/           # React components (posts, comments, forms, etc.)
│   ├── pages/                # Main views (home, profile, login)
│   ├── services/             # Firebase API integration
│   ├── utils/                # Helper functions and model utilities
│   └── App.js                # Main React entry point
├── functions/                # Firebase functions for backend logic
│   ├── index.js
│   └── toxicity.js           # TensorFlow.js model integration
├── package.json              # Project dependencies
├── firebase.json             # Firebase hosting configuration
└── README.md
```

## Installation & Setup

### Prerequisites
- Node.js 18+
- Firebase CLI (`npm install -g firebase-tools`)
- A Firebase project with Authentication and Firestore enabled

### Clone & Install
```bash
git clone <repository-url>
cd safespace
npm install
```

### Environment Variables
Create a `.env` file in the project root with your Firebase config values:

```env
REACT_APP_API_KEY=<your-api-key>
REACT_APP_AUTH_DOMAIN=<your-auth-domain>
REACT_APP_PROJECT_ID=<your-project-id>
REACT_APP_STORAGE_BUCKET=<your-storage-bucket>
REACT_APP_MESSAGING_SENDER_ID=<your-sender-id>
REACT_APP_APP_ID=<your-app-id>
```

### Running Locally
```bash
npm start
```
Frontend will be available at http://localhost:3000.

For Firebase Functions:
```bash
cd functions
npm install
firebase emulators:start
```

### Deployment
To deploy both the frontend and backend:
```bash
firebase deploy
```
This will deploy hosting, authentication, Firestore, and functions as configured in firebase.json.

## Development Notes

- TensorFlow.js runs in-browser, ensuring toxic content is filtered before rendering.
- Running the model client-side keeps moderation fast and private.
- Firebase Auth ensures secure sign-in and user identity handling.
- Posts and comments are stored in Firestore and linked to user IDs.
- Firebase Functions can be extended for additional features like notifications or third-party integrations.
