# Hello, Backboard

## What is Backboard?
Backboard is your entire AI stack in one API. Memory, models, assistants, document processing, and 
more -- all through a single platform. In this demo, we are using just one piece: creating an assistant and having a conversation with it.

## What are we building in this demo?
We are about to create your first AI assistant, start a conversation with it, and get a response. Think of it like building your own ChatGPT, but one you control through code. Three steps, five minutes.

## Prerequisites
- A Backboard account with an API key
- Python 3.7+

### Step 1:
An Assistant is an AI agent with specific instructions. Create one with a simple request:
```python
import asyncio
import os
from backboard import BackboardClient
from dotenv import load_dotenv

load_dotenv()

async def main():
    client = BackboardClient(api_key=os.getenv("BACKBOARD_API_KEY"))

    assistant = await client.create_assistant(
        name="My First Assistant",
        system_prompt="You are a helpful assistant that responds concisely."
    )

    print(f"Created assistant: {assistant.assistant_id}")

asyncio.run(main())
```

### Step 2: Create a Thread
A Thread represents a conversation session. Create one for your assistant:
```python
thread = await client.create_thread(assistant.assistant_id)
print(f"Created thread: {thread.thread_id}")
```

### Step 3: Send a Message (Non-Streaming)
Send a message and wait for the complete response:
```python
response = await client.add_message(
    thread_id=thread.thread_id,
    content="say Hello World",
    stream=False
)
print(f"Assistant: {response.content}")
```

### Run the Script
```
python hello_backboard/main.py
```
