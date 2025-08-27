
## Project Overview

This Android application delivers an AI-powered chatbot running the LLAMA language model locally. The system uses a base model and dynamically loaded adapters to provide efficient, personalized conversational experiences. Android OS resources are utilized to run fine-tuning operations when the device is idle or charging. Key features include a modern chat UI, personalized settings for overlay/app targeting, and on-device privacy.

**Unique Aspects**:

-   Local-first, privacy-focused LLM inference (no cloud dependency)
    
-   Adapter-based extensibility for domain and personalization
    
-   Fine-tunes model efficiently when the device is charging/idle, with minimal user intervention
    

----------

## `technical-architecture.md`

## Technical Stack


| Component                    | Technology                                  | Link                                         |
| ---------------------------- | ------------------------------------------- | -------------------------------------------- |
| Web Application Frontend     | React/Angular/Vue.js, HTML, CSS, JavaScript | Relevant official docs or framework websites |
| Backend Service/Model Server | Node.js/Python (FastAPI, Flask)             | https://fastapi.tiangolo.com/                |
| LLAMA model runner           | llama.cpp/Ollama Backend APIs               | https://github.com/ollama/ollama             |
| Fine-tuning Framework        | LoRA/QLoRA/Unsloth                          | https://github.com/unslothai/unsloth         |
| Overlay and Accessibility    | Browser Extensions, Web Workers             | Browser APIs                                 |

## `architecture-overview.md`

## Solution Architecture

-   The app is structured in modules: UI (chat interface, settings), Service/UI overlay, Model Interaction Layer, Fine-tuning worker.
    
-   Uses Android foreground services to interact with background model processes (Ollama/llama.cpp invoked via JNI or a Termux environment).
    
-   Adapters for LLM are dynamically selected and loaded.
    
-   A background worker schedules fine-tuning when idle/charging and applies trained adapters automatically.
    
-   Communication between Android and model runners is via sockets or local IPC.
    
-   All sensitive data (user chats/fine-tune data) is kept on-device.
    

----------

## `implementation-details.md`

1.  **UI Implementation**: Built using Jetpack Compose for chat interface, list-based message rendering, and app overlay using specialized Android system permissions.
    
2.  **Model Pipeline**: Initial base model (quantized for size) invoked via system shell/JNI interface from within the app. Adapters are modular binary/text files loaded before inference.
    
3.  **Fine-tuning**: Python/C++ scripts integrated using Termux or directly compiled binaries, tracking device charge/state with Android WorkManager API.
    
4.  **Security**: All user data and adapters are sandboxed within app storage.
    
5.  **Overlay Logic**: Accessibility service monitors foreground app and ensures overlay is toggled as per user settings.
    

----------

## `installation.md`

## Prerequisites

-   4GB+ RAM Android device (recommended)
    
-   Android 8.0+ (for best compatibility)
    
-   Sufficient local free storage (at least 4GB for models/adapters)
    

## Installation Steps

1.  Navigate to the website [INSERT HERE]
    
2.  This WebApp will request overlay and accessibility permissions for the application
3.  Download base model and initial adapters through in-app prompts or instructions.
    
5.  Optionally, set up advanced configuration with Termux if running custom/alternative model runners.
    
6.  Follow setup wizard to personalize overlay and fine-tuning preferences.
    

----------

## `user-guide.md`

## Using the App

-   **Chatting**: Type or speak your query. The app uses the base LLM + current adapter context.
    
-   **Personalization**: In settings, select which apps allow the chatbot overlay.
    
-   **Fine-tune Management**: Toggle fine-tuning (when idle/charging), and review or revert adapters in advanced options.
    
-   **Privacy**: All conversations and adapters remain on device; users can wipe data anytime.
    

----------

## `salient-features.md`

-   **LLAMA locally on Android**: true local operation, no external servers/cloud.
    
-   **Adapters**: instant domain-specific or personalized swap-in.
    
-   **Dynamic fine-tuning**: leverages user context when the device is not in use.
    
-   **Modern, minimal chat UI**: optimized for usability and Android look/feel.
    
-   **Overlay settings**: decide where the AI is available, boosting focus & privacy.
    
-   **End-to-end privacy**: all data, models, and AI computation are kept on your device.
