# WhatsApp-Driven Google Drive Assistant

This project is a powerful automation workflow built in [n8n](https://n8n.io/) that connects a WhatsApp chat interface to a user's Google Drive. It allows for file management and document summarization directly from your phone using simple text commands. The workflow is designed to be **secure**, **easy to set up**, and **extensible**.

---

## Features

- **File Management**: `LIST`, `DELETE`, and `MOVE` files within your Google Drive from WhatsApp.
- **AI Summarization**: Use `SUMMARY` to get a concise, AI-generated summary of any `.pdf`, `.docx`, or `.txt` file using the OpenAI API.
- **Secure Operations**: The workflow operates within the authenticated user's Google Drive and includes a confirmation step for destructive actions like `DELETE` to prevent accidents.
- **Audit Logging**: Every command executed is logged in a designated Google Sheet for security and tracking.

---

## Setup and Execution

To run this workflow, you will need:

- [Docker](https://www.docker.com/)
- A [Twilio](https://www.twilio.com/) account (for WhatsApp API)
- Google OAuth credentials
- An OpenAI API key

### 1. Clone Repository

Get the project files onto your local machine:

```bash
git clone https://github.com/YOUR_USERNAME/whatsapp-gdrive-assistant.git
cd whatsapp-gdrive-assistant
```

### 2. Configure Credentials

The workflow requires several secret keys. Create a `.env` file from the provided sample and add your credentials.

```bash
# Create the environment file
cp .env.sample .env
```

Now, open `.env` and fill in your API keys for:

- `TWILIO_ACCOUNT_SID` & `TWILIO_AUTH_TOKEN`
- `GOOGLE_CLIENT_ID` & `GOOGLE_CLIENT_SECRET`
- `OPENAI_API_KEY`
- `AUDIT_LOG_SHEET_ID`

### 3. Run with Docker

The included `docker-compose.yml` file simplifies the setup. This command starts the n8n service:

```bash
docker-compose up
```

### 4. Import Workflow

- Navigate to n8n in your browser at [http://localhost:5678](http://localhost:5678).
- Create a new workflow and select **Import from File**.
- Upload the `n8n/workflow.json` file from this repository.
- Activate the workflow. It is now live and listening for commands.

---

## Command Syntax

Send the following commands to your configured Twilio WhatsApp number:

| Command   | Description                      | Example                                  |
|-----------|----------------------------------|------------------------------------------|
| `LIST`    | Lists all files in a folder      | `LIST /ProjectDocs`                      |
| `DELETE`  | Deletes a specified file         | `DELETE /ProjectDocs/report-v1.pdf`      |
| `MOVE`    | Moves a file to another folder   | `MOVE /ProjectDocs/image.png /Archive`   |
| `SUMMARY` | Generates a summary of a file    | `SUMMARY /ProjectDocs/meeting-notes.docx`|

---

## Project Status & Implementation Notes

This repository provides the **complete structural plan and configuration** for the project as per the task requirements.

**Deliverables Included:**
- `README.md`
- `n8n/workflow.json` (template)
- `.env.sample`
- `docker-compose.yml`

**Implementation Details:**  
The core logic resides within the `workflow.json`. It is designed with distinct nodes for webhook listening, command parsing, routing (via a `SWITCH` node), and executing actions through dedicated Google Drive and OpenAI nodes. Error handling is configured to send user-friendly feedback directly to WhatsApp.

**Next Steps:**  
The final implementation step would be to configure the OAuth2 credentials within the n8n UI and activate the workflow.

---

## License

This project is provided for educational and demonstration purposes.

---

## Contact

For issues or suggestions, please open an [issue](https://github.com/annniE96/WhatsApp-Driven-Google-Drive-Assistant/issues) or submit a pull request.
