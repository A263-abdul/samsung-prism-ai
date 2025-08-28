
# PROJECT OVERVIEW


This project is an **AI-powered chatbot application for Android**, designed to combine **privacy, personalization, and efficiency**. Instead of relying on the cloud, it runs the **LLAMA language model directly on-device**, ensuring that all conversations and user data remain private.

At its core, the system uses a **base model** that is lightweight and optimized for mobile devices. To make the chatbot flexible, it supports **adapters** — small, modular extensions that let the AI quickly switch roles or specialize in certain domains such as _study help, coding assistance, travel planning, or personal wellness_. This adapter-based approach allows the chatbot to adapt instantly without retraining the entire model.

The app also integrates **smart fine-tuning**. Whenever the phone is idle or charging, the system quietly updates active adapters based on the user’s recent interactions. This means the chatbot becomes more **personalized and context-aware over time**, while keeping energy usage and performance optimized

**What makes it special?**
    
-   🧩 **Adapters for flexibility** → switch chatbot roles (study, coding, travel, etc.) instantly.
    
-   ⚡ **Smart fine-tuning** → improves automatically in the background with zero effort
    

----------

# `Technical-architecture`

## Technical Stack


| Component                    | Technology                                  | Link                                         |
| ---------------------------- | ------------------------------------------- | -------------------------------------------- |
| Web Application Frontend     | React/Angular/Vue.js, HTML, CSS, JavaScript | Relevant official docs or framework websites |
| Backend Service/Model Server | Node.js/Python (FastAPI, Flask)             | https://fastapi.tiangolo.com/                |
| LLAMA model runner           | llama.cpp/Ollama Backend APIs               | https://github.com/ollama/ollama             |
| Fine-tuning Framework        | LoRA/QLoRA/Unsloth                          | https://github.com/unslothai/unsloth         |
| Overlay and Accessibility    | Browser Extensions, Web Workers             | Browser APIs                                 |

# `Architecture-overview.md`

## Solution Architecture
### **1. User Interface Layer**

-   Provides a modern **chat interface** with personalization options and quick settings.
    
-   Supports **UI overlay mode**, allowing the assistant to integrate seamlessly across applications.
    
-   Ensures a consistent, responsive experience while remaining lightweight.
    

### **2. Service & Orchestration Layer**

-   Leverages **Android Foreground Services** to maintain persistent interaction with background model processes.
    
-   Manages task scheduling, lifecycle events, and smooth communication between the UI and fine-tuning modules.
    
-   Ensures uninterrupted operation during multitasking and device idle states.
    

### **3. Model Interaction Layer**

-   Interfaces with optimized LLM backends such as **Ollama** or **llama.cpp** through **JNI bridges** or lightweight containerized runtimes (e.g., Termux).
    
-   Dynamically loads and applies **parameter-efficient adapters** (LoRA/PEFT) at runtime without impacting the base model.
    
-   Uses **local IPC or socket-based communication** for low-latency message passing between Android components and model runners.
    

### **4. Fine-Tuning & Adaptation Worker**

-   A **background worker** handles fine-tuning tasks intelligently, triggered only during **idle and charging conditions** to respect battery and thermal limits.
    
-   Incorporates a **job scheduler** that can pause, resume, or checkpoint fine-tuning seamlessly.
    
-   Automatically integrates newly trained adapters into the active model pipeline once training is complete.
    

### **5. Data Privacy & Security Layer**

-   All sensitive data—including user conversations and fine-tuning datasets—remains strictly **on-device**, never leaving the user’s control.
    
-   Adapters, checkpoints, and personal data are **sandboxed and encrypted**, ensuring security even in offline environments.
    
-   Provides **per-user and per-app persona isolation**, enabling customized assistants for different contexts without cross-contamination of data

-   
    

----------

# implementation-details

1.  **UI Implementation**: Built using Jetpack Compose for chat interface, list-based message rendering, and app overlay using specialized Android system permissions.
    
2.  **Model Pipeline**: Initial base model (quantized for size) invoked via system shell/JNI interface from within the app. Adapters are modular binary/text files loaded before inference.
    
3.  **Fine-tuning**: Python/C++ scripts integrated using Termux or directly compiled binaries, tracking device charge/state with Android WorkManager API.
    
4.  **Security**: All user data and adapters are sandboxed within app storage.
    
5.  **Overlay Logic**: Accessibility service monitors foreground app and ensures overlay is toggled as per user settings.
    

----------

# `Installation`

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

# `user-guide.md`

### Using the App

## Welcome to Your AI Chatbot 

-   When you open the app, you are greeted by a **modern chat interface**.
    
-   The chatbot runs **entirely on your device** (LLAMA model).
    

##  Start Chatting 💬

-   Type or speak your question.
    
-   The chatbot answers instantly.
   
   ## Overlay Chat (Anywhere, Anytime) 📱

-   Turn on **Overlay Mode** in settings.
    
-   The chatbot floats over other apps.
## Adapter System 🧩

1.  Adapters are small brain modules that let the chatbot switch between roles (e.g., Study Helper, Coding Buddy, Travel Assistant).
    
2.  They auto fine-tune while charging/idle and can be updated, reverted, or deleted anytime
##  Smart Fine-tuning ⚡

1.  The chatbot automatically fine-tunes active adapters when the device is charging or idle, improving personalization without user effort.
    
2.  Users can review, accept, revert, or delete fine-tuned updates anytime for full control.
----------

## `salient-features.md`

-   **LLAMA locally on Android**: true local operation, no external servers/cloud.
    
-   **Adapters**: instant domain-specific or personalized swap-in.
    
-   **Dynamic fine-tuning**: leverages user context when the device is not in use.
    
-   **Modern, minimal chat UI**: optimized for usability and Android look/feel.
    
-   **Overlay settings**: decide where the AI is available, boosting focus & privacy.
    
-   **End-to-end privacy**: all data, models, and AI computation are kept on your device.
