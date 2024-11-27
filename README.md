# Omi Memory Keeper: AI-Powered Life Journal

## Description
Omi Memory Keeper is an AI-powered life journal that uses real-time transcription data from the Omi wearable device to automatically capture and reflect on conversations. The app helps users log meaningful moments, track emotional states, and gain insights into their personal growth. By turning everyday interactions into valuable memories, the app enables users to gain a fresh perspective on their life journey.

---

## Features
- **Automatic Memory Logging**: Capture significant moments in conversations and store them in a searchable timeline.
- **Emotion Tracking**: Detect mood fluctuations through sentiment analysis and track emotional patterns over time.
- **Personalized Reflection**: Get AI-generated summaries and prompts to help users reflect on past conversations and grow personally.
- **Memory Reels**: Create highlight reels of memories and share them with loved ones.
- **Progress Insights**: Track mood, emotional well-being, and personal development over time with interactive dashboards.

---

## Built With
- **Languages**: Python, JavaScript
- **Frameworks**: Flask (Backend), React (Frontend)
- **Platforms/Cloud Services**: Google Cloud, Firebase
- **APIs**: Omi API, Google Natural Language API
- **Databases**: PostgreSQL
- **Other Technologies**: Docker, TensorFlow, NLTK (Natural Language Toolkit)

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/omi-memory-keeper.git
   cd omi-memory-keeper
   ```

2. Set up the backend:
   - Make sure you have Python 3.x installed.
   - Install the required dependencies:
     ```bash
     pip install -r requirements.txt
     ```

3. Set up the frontend:
   - Make sure you have Node.js and npm installed.
   - Navigate to the `client` folder and install the necessary packages:
     ```bash
     cd client
     npm install
     ```

4. Set up PostgreSQL:
   - Install and configure PostgreSQL, then create a database called `omi_memory_keeper`.
   - Run the database migrations:
     ```bash
     python manage.py db upgrade
     ```

5. Configure your environment variables (e.g., for Omi API, Google Cloud credentials, etc.).

6. Run the app:
   - Start the backend:
     ```bash
     python app.py
     ```
   - Start the frontend:
     ```bash
     npm start
     ```

---

## Sample Code

Here is a sample of how we use the **Google Natural Language API** to analyze sentiment from transcribed conversations and determine the user's emotional state:

### Python (Backend) - Sentiment Analysis

```python
from google.cloud import language_v1
from google.cloud.language_v1 import enums

def analyze_sentiment(text):
    client = language_v1.LanguageServiceClient()

    document = language_v1.Document(content=text, type_=enums.Document.Type.PLAIN_TEXT)
    sentiment = client.analyze_sentiment(request={'document': document}).document_sentiment

    return sentiment.score, sentiment.magnitude

# Example usage:
text = "I am feeling really happy today, everything seems to be going well."
score, magnitude = analyze_sentiment(text)
print(f"Sentiment Score: {score}, Magnitude: {magnitude}")
```

This function uses the Google Cloud Natural Language API to analyze the sentiment of a given text. The score indicates whether the sentiment is positive or negative, and the magnitude shows the strength of the sentiment.

---

### React (Frontend) - Displaying Emotional Insights

```javascript
import React, { useState, useEffect } from 'react';

const EmotionDashboard = () => {
  const [emotionData, setEmotionData] = useState([]);

  useEffect(() => {
    fetch('/api/emotion-data')
      .then(response => response.json())
      .then(data => setEmotionData(data));
  }, []);

  return (
    <div className="emotion-dashboard">
      <h1>Emotional Insights</h1>
      <ul>
        {emotionData.map((entry, index) => (
          <li key={index}>
            <strong>{entry.date}:</strong> {entry.emotion} (Strength: {entry.magnitude})
          </li>
        ))}
      </ul>
    </div>
  );
};

export default EmotionDashboard;
```

This simple React component fetches emotional insights from the backend and displays them on the user’s dashboard. It shows the emotions and their associated strength (magnitude) based on the conversation logs.

---

## Challenges
- **Sentiment Analysis Accuracy**: Ensuring that the AI correctly identifies emotions in nuanced conversations.
- **User Privacy**: Implementing strict data privacy measures to ensure that users' conversations and personal data are kept secure.
- **Real-Time Transcription**: Handling large volumes of transcription data and processing them efficiently.

---

## Accomplishments
- Successfully integrated Omi's real-time transcription feature to automatically log memories.
- Created a seamless UI that allows users to track emotions, view past memories, and gain personal insights.
- Developed a sentiment analysis engine capable of detecting emotional shifts in user conversations.

---

## What We Learned
- The importance of building a strong AI model for accurate sentiment analysis in real-world scenarios.
- How to manage and display large datasets (e.g., emotion tracking and memory logs) in a user-friendly way.
- User feedback is crucial for shaping features like memory summarization and emotional tracking.

---

## What's Next
- **Expanded AI Insights**: We plan to develop more advanced AI-driven recommendations for personal growth and mental well-being.
- **Memory Sharing**: Add features to share memories or emotional insights with close friends or family in a private and meaningful way.
- **Mobile App**: Develop a mobile app to make it easier for users to access and interact with their memories and emotional data on the go.