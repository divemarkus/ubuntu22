
# Model Context Protocol (MCP)

## Overview
The Model Context Protocol (MCP) is a communication standard designed to facilitate seamless interaction between different AI models and services. It enables Open Web UI to integrate both locally downloaded models (via tools like Ollama) and hosted models from external providers such as OpenAI, creating a unified interface for diverse AI functionalities.

## Key Features
- **Seamless Integration**: MCP allows various AI models and services to work together within the Open Web UI environment.
- **Local and Cloud Models**: Supports both locally downloaded models (e.g., using Ollama) and cloud-based models (e.g., OpenAI).
- **Enhanced Functionality**: By connecting multiple AI tools, MCP enhances the overall capabilities of Open Web UI, making it a versatile platform for AI-driven tasks.

## Use Cases
1. **Mixed Model Deployment**:
   - Deploy locally downloaded models alongside hosted ones within a single interface.
   - Example: Using GPT-3.5 via Ollama and integrating with OpenAI's API for specialized tasks.

2. **Multi-Tool Integration**:
   - Integrate multiple AI tools into one workflow, enhancing productivity.
   - Example: Automate data analysis by combining image recognition (via Frigate) with natural language processing (via OpenAI).

## Architecture
The architecture of MCP within the Open Web UI ecosystem can be visualized as follows:

```
          +----------------+       +----------------+
          |                |       |                |
          |   Open Web UI  |       |      Frigate   |
          |                |       |                |
          +----------------+       +----------------+
                 ||                     ||
                 ||                     ||
                 \|/                    \|/
             +---+----+           +-----+-----+
             |                         |
             |                         |
             |                         |
   +--------+---------+     +--------+-------+
   |        |         |     |        |       |
   |  Local Models    |     |  External APIs |
   | (e.g., Ollama)   |     | (e.g., OpenAI) |
   |        |         |     |        |       |
   +--------+---------+     +--------+-------+
             ||                     ||
             ||                     ||
             \|/                    \|/
          +----------------+       +----------------+
          |                |       |                |
          |    Portainer   |       |     Jellyfin   |
          |                |       |                |
          +----------------+       +----------------+
```

This diagram illustrates how MCP connects various components, allowing them to interact and share data within the Open Web UI environment.

## Integration Example
Here's a basic example of how MCP can be used to connect different AI services within Open Web UI:

```python
from openwebui import ModelContext

# Initialize the model context
context = ModelContext()

# Add local model (e.g., Ollama)
local_model = context.add_local_model("ollama://gpt-3.5")

# Add external API (e.g., OpenAI)
openai_model = context.add_api_model("openai", "your-api-key")

# Use models together
response = context.request(
    model_id="mixed-model",
    prompt="Analyze this image and describe it in detail.",
    image_path="/path/to/image.jpg"
)

print(response)
```

This example demonstrates how MCP can orchestrate requests across multiple AI services, enhancing the capabilities of Open Web UI. 

----

Also, check-out https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/

## Conclusion
MCP is a vital component of Open Web UI, enabling the integration of diverse AI models and services. By supporting both local and external models, MCP provides developers with a powerful toolset to build sophisticated AI-driven applications. For more detailed information and specifications, please refer to the official documentation or resources provided by Open Web UI.
