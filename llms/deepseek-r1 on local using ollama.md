**What is DeepSeek-R1?**  
DeepSeek-R1 is an open-source, free AI model designed for tasks requiring extensive reasoning, such as programming problem-solving, advanced mathematics, and logical processes. Its main advantage is that it runs entirely on your local machine, eliminating the need to send data to external servers, ensuring privacy and reducing monthly costs associated with other popular providers.

---

## 1. Why is DeepSeek-R1 special?

### 1. Reinforcement Learning (RL) vs. Supervised Training

DeepSeek-R1 "learns" by solving problems through trial and error, rather than relying heavily on traditionally labeled datasets. This enhances its self-verification ability and long-range reasoning skills.

### 2. Cost Efficiency

When run locally, you can use "distilled" versions ranging from 1.5B to 70B parameters, which are compatible with common GPUs (or with some optimization, on high-end CPUs). This avoids expensive monthly subscriptions or per-token costs.  
The full-scale version reaches up to 671B parameters, suitable for highly complex tasks (requiring high-end hardware $$$).

### 3. Open-Source Flexibility

Being open-source means no restrictions on integration into your projects. You can fine-tune it, combine it with other libraries, or even create your own web service based on DeepSeek-R1.

---

## 2. Prerequisites for Installing and Running DeepSeek-R1

- Basic knowledge of the terminal/command line.
    
- A Linux/macOS system (or Windows with WSL2).
    
- Docker installed if planning to use the web interface.
    
- Ollama to download and run the model locally (installation guide included below).
    

---

## 3. Installing Ollama

Ollama is a tool that allows you to manage and run language models locally, functioning similarly to "Docker" but for AI models.

### Installation:

#### On Linux/WSL2:

```
curl -fsSL https://ollama.com/install.sh | sh
ollama -v  # Verify the installed version
```

#### On macOS:

```
brew install ollama
brew services start ollama  # Start Ollama as a background service
ollama -v  # Verify the installed version
```

---

## 4. Downloading DeepSeek-R1 with Ollama

Choose the "distilled" model version that best suits your GPU (or CPU):

- **1.5B parameters (approx. 1.1GB):**
    
    ```
    ollama run deepseek-r1:1.5b
    ```
    
- **8B parameters (approx. 4.7GB):**
    
    ```
    ollama run deepseek-r1:8b
    ```
    
- **14B parameters (requires +12GB VRAM):**
    
    ```
    ollama run deepseek-r1:14b
    ```
    
- **32B parameters (requires +16GB VRAM):**
    
    ```
    ollama run deepseek-r1:32b
    ```
    
- **70B parameters (requires +24GB VRAM):**
    
    ```
    ollama run deepseek-r1:70b
    ```
    
- **Full 671B version (for high-end hardware with +300GB VRAM):**
    
    ```
    ollama run deepseek-r1:671b
    ```
    

Once you run DeepSeek, it will start downloading the model, and you will see a terminal output confirming the process.

### **Tip:** If your PC has limited resources, start with the 1.5B version and gradually test larger models. The 1.5B model is around 1GB, has some limitations, but remains functional. You can explore other compatible models on the Ollama website.

---

## 5. Setting Up the Web Interface with Docker

For those who prefer a user-friendly UI, you can use Open Web UI to interact visually with DeepSeek-R1.

### **Steps:**

1. Install Docker following the instructions at [https://glovoapp.atlassian.net/wiki/spaces/TECH/pages/4473684004](https://glovoapp.atlassian.net/wiki/spaces/TECH/pages/4473684004) (download the version for your OS).
    
2. Run the Open Web UI container:
    

- Linux/WSL2
    

```
docker run -d -p --network=host \\
  -v open-webui:/app/backend/data \\
  -e OLLAMA_BASE_URL=http://127.0.0.1:11434 \\
  --name open-webui \\
  --restart always \\
  ghcr.io/open-webui/open-webui:main  
```

- Mac using Colima
    

```
docker run -d --network=host \
  -v open-webui:/app/backend/data \
  -e OLLAMA_BASE_URL="http://192.168.5.2:11434" \
  --name open-webui \
  --restart=always \
  ghcr.io/open-webui/open-webui:main
```

**Note:** Some options, like --network=host, are for development mode and allow your PC and the Docker container to share a network.

3. Access the UI at http://localhost:8080.
    
4. Create an admin account to manage the platform.
    
5. Select deepseek-r1:1.5b and start chatting with DeepSeek-R1 without sending data to remote servers.
    

---

## 6. Testing DeepSeek-R1 on Your Machine

Once Ollama has downloaded the model and the UI is set up (optional), you can start asking questions via the terminal or UI.

To run via the terminal:

```
ollama run deepseek-r1:1.5b
```

---

## 7. Integrating DeepSeek-R1 into Your Projects

DeepSeek-R1 supports integration.

Ollama can function as an OpenAI-compatible endpoint, allowing your Python scripts to communicate with your local instance:

```
import openai

# Connect to Ollama
client = openai.Client(
    base_url="http://localhost:11434/v1",
    api_key="ollama"
)

response = client.chat.completions.create(
    model="deepseek-r1:1.5b",  # Replace with the chosen version
    messages=[{"role": "user", "content": "Make a 'Hello World' with Go"}],
    temperature=0.7
)
```

To get more information on how to interact with the Ollama API, you can use the following link:

[https://glovoapp.atlassian.net/wiki/spaces/ITS/pages/5128519765](https://glovoapp.atlassian.net/wiki/spaces/ITS/pages/5128519765)