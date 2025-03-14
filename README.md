# Building a Sassy AI Chatbot with Hyperbolic API

## Introduction
In this tutorial, we will build a fun and sassy AI chatbot using the **Hyperbolic API**. This chatbot will generate witty, sarcastic, and humorous responses to user messages. We will cover everything from setting up the environment to integrating the chatbot with the Hyperbolic Labs API. By the end, you will have a fully functional chatbot that can be deployed on any Linux server.

## Prerequisites
Before we begin, make sure you have the following:
- A **Linux server** (Ubuntu recommended)
- **Python 3.6+** installed
- An API key from **Hyperbolic Labs**
- Basic knowledge of Python and Flask

## Step 1: Setting Up the Environment
First, update your system and install required packages:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3 python3-pip python3-venv -y
```

Then, clone the repository and create a virtual environment:

```bash
git clone https://github.com/yourusername/sassy-chatbot.git
cd sassy-chatbot
python3 -m venv venv
source venv/bin/activate
```

Install the required dependencies:

```bash
pip install flask requests
```

## Step 2: Writing the Chatbot Code
Now, let's create our chatbot using Flask. Open a new file `chatbot.py` and add the following code:

```python
from flask import Flask, request, jsonify
import requests
import random

app = Flask(__name__)

API_KEY = "YOUR_HYPERBOLIC_API_KEY"
HYPERBOLIC_ENDPOINT = "https://api.hyperbolic.com/chat"

responses = [
    "Oh wow, another human thinking they're special. Cute.",
    "Try harder. Even my toaster has better comebacks.",
    "That was a joke, right? Please tell me it was a joke.",
    "Wow, you're really pushing the limits of my patience, huh?",
    "I've seen smarter responses from a brick wall."
]

@app.route("/chat", methods=["POST"])
def chat():
    data = request.json
    user_message = data.get("message", "")
    
    # 50% chance to use predefined response or API
    if random.random() < 0.5:
        return jsonify({"response": random.choice(responses)})
    
    response = requests.post(HYPERBOLIC_ENDPOINT, json={"input": user_message}, headers={"Authorization": f"Bearer {API_KEY}"})
    return jsonify(response.json())

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

Replace `YOUR_HYPERBOLIC_API_KEY` with your actual API key.

## Step 3: Running the Chatbot
Now, run the chatbot server:

```bash
python chatbot.py
```

You should see output similar to:

```
 * Running on http://0.0.0.0:5000
```

To test the chatbot, use `curl` or Postman:

```bash
curl -X POST http://127.0.0.1:5000/chat -H "Content-Type: application/json" -d '{"message": "Roast me!"}'
```

## Step 4: Deploying on GitHub
To allow others to use and modify the chatbot, upload the project to GitHub:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/sassy-chatbot.git
git push -u origin main
```

## Step 5: Posting the Tutorial on X
Now that your chatbot is working, write a post on X (Twitter) and tag `@hyperbolic_labs` and `@hyperbolic_eacc`.

### Example Tweet:
🚀 Built a sassy AI chatbot using @hyperbolic_labs API! It roasts users with witty responses and is now open-source! Check it out here: [GitHub Link] #AI #HyperbolicLabs #Chatbot

## Conclusion
Congratulations! You have successfully built and deployed a sassy AI chatbot using **Hyperbolic API**. Now, share your tutorial and earn **XP** in the Hyperbolic Labs campaign!

