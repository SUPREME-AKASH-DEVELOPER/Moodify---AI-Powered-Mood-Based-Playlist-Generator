# Moodify---AI-Powered-Mood-Based-Playlist-Generator


```markdown
# Moodify - AI-Powered Mood-Based Playlist Generator

## Inspiration

In today’s fast-paced world, finding the right music that matches our current emotional state can be challenging. Moodify was inspired by the desire to bridge the gap between our feelings and the music we listen to. We aimed to create a personalized music experience that evolves with our emotions, using advanced AI technology to enhance how we interact with music.

## What it Does

Moodify detects your mood through facial expressions or text input and generates a personalized playlist that matches your emotional state. By leveraging real-time AI, Moodify ensures that your music aligns with how you feel at any moment, whether you're happy, sad, or excited. The platform curates the perfect soundtrack to enhance your experience.

## How We Built It

### 1. Setup Development Environment

1. **Install Node.js and npm:**
   Download and install Node.js from [nodejs.org](https://nodejs.org). npm (Node Package Manager) is included with Node.js.
   ```bash
   node -v
   npm -v
   ```

2. **Install Python:**
   Download and install Python from [python.org](https://www.python.org).

3. **Setup Convex Account:**
   Sign up for Convex and set up your account from [Convex](https://convex.dev).

### 2. Create Project Structure

1. **Initialize the Project:**
   ```bash
   mkdir moodify
   cd moodify
   npm init -y
   ```

2. **Set Up React Frontend:**
   ```bash
   npx create-react-app frontend
   cd frontend
   npm install tailwindcss
   npx tailwindcss init
   ```

   Configure Tailwind CSS by adding it to `tailwind.config.js` and importing it in `src/index.css`.

3. **Set Up Backend:**

   Create a directory for your backend:
   ```bash
   mkdir backend
   cd backend
   npm init -y
   npm install express convex
   ```

   Create a basic Express server in `backend/server.js`:
   ```javascript
   const express = require('express');
   const app = express();
   const port = 5000;

   app.use(express.json());

   app.get('/', (req, res) => {
     res.send('Moodify Backend Running');
   });

   app.listen(port, () => {
     console.log(`Server running at http://localhost:${port}`);
   });
   ```

### 3. Implement Mood Detection

1. **Integrate TensorFlow.js for Facial Recognition:**
   ```bash
   npm install @tensorflow/tfjs @tensorflow-models/facemesh
   ```

   Add mood detection logic to your React app in `src/components/MoodDetector.js`:
   ```javascript
   import React, { useEffect } from 'react';
   import '@tensorflow/tfjs';
   import { FaceMesh } from '@tensorflow-models/facemesh';

   function MoodDetector() {
     useEffect(() => {
       async function loadModel() {
         const model = await FaceMesh.load();
         // Load and use the model for mood detection
       }

       loadModel();
     }, []);

     return <div>Loading...</div>;
   }

   export default MoodDetector;
   ```

2. **Integrate Sentiment Analysis:**
   Choose a sentiment analysis API (e.g., Google Cloud Natural Language API).

   Install the client library:
   ```bash
   npm install @google-cloud/language
   ```

   Implement text sentiment analysis in your backend:
   ```javascript
   const { LanguageServiceClient } = require('@google-cloud/language');
   const client = new LanguageServiceClient();

   async function analyzeSentiment(text) {
     const document = {
       content: text,
       type: 'PLAIN_TEXT',
     };

     const [result] = await client.analyzeSentiment({ document });
     return result.documentSentiment.score;
   }
   ```

### 4. Integrate Music API

1. **Spotify API Integration:**
   Set up Spotify API credentials from the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).

   Install Spotify Web API Node package:
   ```bash
   npm install spotify-web-api-node
   ```

   Add functionality to fetch playlists based on mood:
   ```javascript
   const SpotifyWebApi = require('spotify-web-api-node');
   const spotifyApi = new SpotifyWebApi({
     clientId: 'YOUR_SPOTIFY_CLIENT_ID',
     clientSecret: 'YOUR_SPOTIFY_CLIENT_SECRET',
   });

   async function getPlaylist(mood) {
     const playlists = await spotifyApi.searchPlaylists(mood);
     return playlists.body;
   }
   ```

### 5. Connect Frontend and Backend

1. **Set Up API Endpoints:**
   Define endpoints in your Express backend to handle requests from your React frontend:
   ```javascript
   app.post('/api/mood', async (req, res) => {
     const { mood } = req.body;
     const playlist = await getPlaylist(mood);
     res.json(playlist);
   });
   ```

2. **Fetch Data in React App:**
   Use Axios or Fetch API to call your backend API from the React frontend:
   ```javascript
   import axios from 'axios';

   async function fetchPlaylist(mood) {
     const response = await axios.post('/api/mood', { mood });
     return response.data;
   }
   ```

### 6. Deploy the Application

1. **Prepare for Deployment:**
   Build the React app for production:
   ```bash
   cd frontend
   npm run build
   ```

   Move the build files to your backend’s public directory and configure Express to serve them.

2. **Deploy on a Platform (e.g., Heroku, Vercel):**

   For Heroku:
   ```bash
   heroku create
   git add .
   git commit -m "Deploy Moodify"
   git push heroku main
   ```

   For Vercel, deploy the React app and backend separately, configuring environment variables and build settings as needed.

## Challenges We Ran Into

- **Real-Time Mood Detection:** Ensuring accurate mood detection while maintaining a seamless user experience was a significant challenge. Fine-tuning the facial recognition model and sentiment analysis for real-time performance required substantial effort.
- **API Integration:** Integrating with external music APIs and managing real-time playlist updates posed technical challenges, particularly in balancing performance and responsiveness.

## Accomplishments That We're Proud Of

- **Seamless Integration:** Successfully integrated real-time mood detection with music playlist generation, providing users with a unique and personalized music experience.
- **User Experience:** Developed an intuitive interface that allows users to easily interact with the mood detection features and enjoy curated playlists instantly.
- **Real-Time Performance:** Achieved real-time performance with Convex, ensuring smooth updates and responsiveness.

## What We Learned

- **AI Integration:** Gained valuable insights into combining AI for facial recognition and sentiment analysis with real-time data handling.
- **User-Centric Design:** Learned the importance of creating an intuitive user interface that effectively communicates complex functionalities in a user-friendly manner.
- **API Management:** Developed skills in managing third-party APIs and handling real-time data synchronization across different services.

## What’s Next for Moodify

- **Enhanced Mood Detection:** Plan to improve the accuracy of mood detection by incorporating additional emotion recognition algorithms and expanding language support for text analysis.
- **Feature Expansion:** Explore adding new features such as mood-based recommendations for podcasts and ambient sounds.
- **User Feedback:** Collect and analyze user feedback to refine the user experience and introduce new functionalities that cater to user needs.


Feel free to adjust the links and image URLs to match your actual resources. Let me know if there's anything else you’d like to add or tweak!
