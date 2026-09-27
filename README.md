
# AI Digital Twin — Shashank MN

An interactive, AI-powered career assistant that represents **Shashank MN** and answers questions about his education, technical skills, projects, certifications, and professional background. Instead of browsing a static resume, visitors can explore his profile through a conversational interface.

## Features

- **Career-focused chat:** Ask natural-language questions about Shashank's background, skills, and experience.
- **Profile-aware responses:** The assistant receives a professional summary and extracted LinkedIn PDF text as context.
- **LLM integration:** Uses Google's Gemini API through an OpenAI-compatible Python client, with the model name configured in `app.py`.
- **Tool-calling workflow:** The app supports tool calls and routes their results back to the model. The system prompt instructs the assistant to capture contact requests and unanswered questions; the implementation of those actions depends on `tools.py`.
- **Custom Gradio UI:** Responsive styling, light/dark palettes, example questions, and input-focus behavior through CSS and JavaScript.
- **Scoped answers:** The assistant is instructed to stay on professional topics and avoid inventing unknown information.

## Tech Stack

**Python · Gradio · Google Gemini API · OpenAI Python SDK · pypdf · python-dotenv · CSS · JavaScript**

## Project Structure

```text
.
├── app.py             # Gradio chat interface and LLM/tool-calling loop
├── context.py         # System prompt and profile-context loading
├── styles.py          # Custom CSS, JavaScript, and example questions
├── tools.py           # Tool definitions and handlers (required; not included in supplied files)
├── linkedin.pdf       # LinkedIn profile used for context
├── summary.txt        # Professional profile summary
├── requirements.txt   # Python dependencies
└── README.md
```

## How It Works

1. `context.py` extracts text from `linkedin.pdf` and reads `summary.txt`.
2. It builds a system prompt instructing the AI to represent Shashank's professional profile.
3. `app.py` initializes an OpenAI-compatible client pointing to Google's Gemini endpoint.
4. Gradio passes each visitor message and conversation history to the chat function.
5. The model generates an answer; if it requests tools, `handle_tool_calls` executes them and the results are returned to the model before the final response.
6. `styles.py` provides the chat interface's visual design and suggested questions.

## Run Locally

**Prerequisites:** Python 3.10+ (recommended), a Google Gemini API key, and the project's `tools.py` module.

1. Clone the repository and navigate into the project directory.
2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the project root:

   ```dotenv
   GOOGLE_API_KEY=your_google_api_key_here
   ```

4. Ensure `app.py`, `context.py`, `styles.py`, `tools.py`, `linkedin.pdf`, and `summary.txt` use these filenames and are in the same directory.
5. Check the `MODEL_NAME` setting in `app.py` against a model identifier available to your Gemini API account. The provided code currently sets it to `gemini-3.6-flash`; this README does not verify that identifier's availability.
6. Start the application:

   ```bash
   python app.py
   ```

Open the Gradio URL printed in the terminal. The provided application calls `launch(..., share=True)`, which also requests a temporary public share link.

> **Important:** `app.py` imports `tools` and `handle_tool_calls` from `tools.py`. That module was not among the uploaded files, so the application will not start until it is supplied or the tool integration is removed. The contact/question capture behavior cannot be confirmed without that module.

## Example Questions

- Tell me about your background and experience.
- What kinds of projects are you working on now?
- What are your strongest technical skills?
- How can I get in touch with you?

## Deployment Notes

The existing `README.md` includes Gradio Spaces metadata, so the project can be prepared for a Hugging Face Space using the Gradio SDK. Make sure the required source and profile files are present and set `GOOGLE_API_KEY` as a Space secret. Avoid committing `.env` or other credentials.

The app loads profile information into the model context and uses a public share link when run as supplied. Review personal information and any contact-capture implementation before deploying publicly.

## Author

**Shashank Nag MN**  
[GitHub](https://github.com/MN-SHASHANK) · [LinkedIn](https://www.linkedin.com/in/mnshashanknag/)

