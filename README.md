
# Code Interpreter with AI Error Analysis

A FastAPI service that executes Python code, returns its
output or traceback, and uses an LLM to identify error
line numbers when execution fails.

## Features

- POST /code-interpreter endpoint
- Python execution with captured output
- Original traceback returned on errors
- AI-powered error line analysis through AI Pipe
- Pydantic response validation
- CORS support
- Health-check endpoint

## Requirements

- Python 3.12
- An AI Pipe API token for AI error analysis

## Install locally

Create and activate a virtual environment, then install
the dependencies:

    python3 -m venv .venv
    source .venv/bin/activate
    pip install -r requirements.txt

On Windows, activate the environment with:

    .venv\Scripts\activate

## Configure the API token

Set your token in the terminal before starting the server.

macOS/Linux:

    export AIPIPE_TOKEN="your-token-here"

Windows PowerShell:

    $env:AIPIPE_TOKEN="your-token-here"

Never commit your real token to Git.

## Run the server

    uvicorn main:app --reload

Open the interactive API documentation at:

    http://127.0.0.1:8000/docs

## Example request

POST /code-interpreter

    {
      "code": "x = 5\ny = 10\nprint(x + y)"
    }

Expected response:

    {
      "error": [],
      "result": "15\n"
    }

## Deployment

Deploy this repository as a Render Web Service.

Build command:

    pip install -r requirements.txt

Start command:

    uvicorn main:app --host 0.0.0.0 --port $PORT

Set AIPIPE_TOKEN in the Render environment variables.

## Security

This educational implementation uses exec() and is not
safe for unrestricted execution of untrusted code.
Production deployments require an isolated sandbox.
