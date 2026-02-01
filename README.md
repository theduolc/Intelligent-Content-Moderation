# Intelligent Content Moderation (PoC)<br>

Description: A user uploads a picture and it gets analyzed with AI<br>
 
+ run Terraform commands: init -> plan -> apply <br>
+ create a IAM role and put the policy in found in policy.json<br>
+ upload a picture file to S3 bucket <br>
+ watch cloudwatch for success or error messages<br>
+ go to ECS and look for new tasks<br>

# Intelligent Content Moderation

A lightweight proof-of-concept application that uses AI to analyze uploaded images for content moderation purposes.

**Current status**: Early prototype / MVP

## What it does

Users can upload an image → the system analyzes it using modern AI vision models → returns moderation results (e.g. safe / unsafe, detected categories like nudity, violence, hate symbols, drugs, etc.).

Goal: Demonstrate intelligent, automated content moderation that can be integrated into platforms, forums, messengers or marketplaces.

## Features (current / planned)

- Image upload via web interface
- AI-based content analysis (multi-label classification + severity scoring)
- Simple result visualization (tags + confidence scores)
- Extensible for text + image multimodal moderation (future)
- Easy to swap AI backends / models

## Tech Stack

- Backend: Python (FastAPI / Flask planned)
- AI: Vision language models (e.g. LLaVA, Florence-2, CLIP-based moderation, or moderated fine-tuned models)
- Frontend: Basic HTML + JavaScript (or React/Vue later)
- Deployment: Docker support planned

## Quick Start

### Prerequisites

- Python 3.10+
- Git
- (Optional) Docker

### 1. Clone the repository

git clone https://github.com/theduolc/Intelligent-Content-Moderation.git
cd Intelligent-Content-Moderation


# Install dependencies

Recommended: use uv or poetry
+ pip install -r requirements.txt

or if using uv (faster)
+ uv pip install -r requirements.txt


# Run the application

Development mode
python app.py
or
python -m uvicorn main:app --reload    # if using FastAPI

Open your browser at:
→ http://localhost:8000 (or port shown in terminal)

# Usage

+ Open the web interface
+ Drag & drop or choose an image
+ Wait for the AI analysis (~1–8 seconds depending on model & hardware)
+ See moderation results
