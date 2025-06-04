## 🔧 Lesson: Implementing Groq for High-Speed LLM Inference

### 🧠 Learning Objectives

By the end of this lesson, learners will be able to:

* Understand what Groq is and what makes it unique.
* Set up access to the Groq API.
* Make a simple Python script to generate text with Groq-hosted models.
* Compare Groq’s speed and response to other LLM APIs.

---

## 🧰 Prerequisites

* Python 3.x installed
* `pip` installed
* Basic knowledge of APIs and Python
* Groq API Key (create an account at [https://console.groq.com](https://console.groq.com))

---

## 1️⃣ What is Groq?

Groq is a company offering **extremely fast** inference for large language models (LLMs), powered by their custom hardware (LPU - Language Processing Units).
They host models like:

* **Meta's LLaMA 3**
* **Mistral’s Mixtral**
* **Gemma** by Google

Groq's edge? Speed. You get 100+ tokens per second — great for real-time applications.

---

## 2️⃣ Setting Up Groq

### Step 1: Get an API Key

* Go to [https://console.groq.com](https://console.groq.com)
* Create an account or log in
* Copy your **API key** from the dashboard

---

## 3️⃣ Installing Required Python Packages

```bash
pip install requests python-dotenv
```

> Optional: Store your API key securely in a `.env` file

**`.env`**

```env
GROQ_API_KEY=your_api_key_here
```

---

## 4️⃣ Python Code: Call Groq API

```python
import os
import requests
from dotenv import load_dotenv

# Load API key from .env
load_dotenv()
API_KEY = os.getenv("GROQ_API_KEY")

# Choose your model
MODEL = "llama3-70b-8192"  # Options: llama3-70b-8192, mixtral-8x7b-32768, gemma-7b-it

# Set up request headers and endpoint
headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}
url = "https://api.groq.com/openai/v1/chat/completions"

# Define the user prompt
prompt = "Explain quantum computing like I'm 5."

# Construct payload
payload = {
    "model": MODEL,
    "messages": [
        {"role": "system", "content": "You are a friendly tutor."},
        {"role": "user", "content": prompt}
    ],
    "temperature": 0.7,
    "max_tokens": 300
}

# Make request
response = requests.post(url, headers=headers, json=payload)
result = response.json()

# Print response
print(result["choices"][0]["message"]["content"])
```

---

## 5️⃣ Customization Tips

* `temperature`: Controls creativity (0 = precise, 1 = creative)
* `max_tokens`: Response length
* Try other models: swap `"model"` field

---

## 6️⃣ Optional: Streaming Response (Advanced)

You can also stream responses by setting `stream=True` in the payload and parsing chunks. Let me know if you want to add that.

---

## 7️⃣ Use Cases

You can build:

* **Chatbots**
* **Writing assistants**
* **Real-time coding helpers**
* **Language tutors**

Groq is especially good for apps that need **instant response**.

---

## 🧪 Homework / Practice

* Try writing a Python function `chat_with_groq(prompt, model="llama3-70b-8192")`
* Build a basic Flask web app that lets users chat with the model
* Compare latency between Groq and OpenAI

---

## 📚 Further Reading

* [Groq API Docs](https://console.groq.com/docs)
* [OpenAI Compatibility](https://console.groq.com/docs/guides/openai-compatible-api)
* Groq blog for performance benchmarks

---

