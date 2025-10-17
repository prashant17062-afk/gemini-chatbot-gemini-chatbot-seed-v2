# Gemini AI Chatbot

## Summary
This project delivers a functional web-based AI chatbot that leverages the Google Gemini API. It allows users to input their Google Gemini API key, save it locally, and then interact with the `gemini-pro` model in real-time. The application is designed to be mobile-responsive and styled with Bootstrap, providing a clean and intuitive user interface. It demonstrates a complete client-side implementation of an AI chatbot, including API key management, chat message display, a typing indicator, and robust error handling.

## Setup
To set up and run this application:

1.  **Save the file:** Save the provided `index.html` content into a file named `index.html` on your local machine.
2.  **Open in browser:** Open the `index.html` file using any modern web browser (e.g., Chrome, Firefox, Edge). There is no server-side component required; it runs entirely in the browser.
3.  **Obtain a Gemini API Key:** You will need a Google Gemini API key. You can obtain one from the Google AI Studio or Google Cloud Console.

## Usage
1.  **Enter API Key:** Upon opening the `index.html` file, you will see an input field labeled "Enter your Google Gemini API key". Paste your API key into this field.
2.  **Save API Key:** Click the "Set API Key" button. The key will be securely saved in your browser's `localStorage`. The "API Key Status" will change to "Set (Ready to chat)", and the chat input field will become enabled.
    *   *Note:* The key remains in `localStorage` across browser sessions for convenience. You can clear it by deleting the content in the input field and clicking "Set API Key" again, or by clearing your browser's local storage for the page.
3.  **Start Chatting:** Type your message into the "Type your message..." input field and click the "Send" button or press `Enter`.
4.  **View Responses:** Your message will appear in the chat, followed by an "AI is typing..." indicator. Shortly after, the Gemini AI's response will appear in the chat.
5.  **Error Handling:** If there's an issue with the API key (e.g., invalid, expired) or a network problem, an appropriate error message will be displayed in the chat interface.

## Main Code Logic

The core functionality of the chatbot is implemented in the `script` section of the `index.html` file:

*   **DOM Loading:** An `DOMContentLoaded` event listener ensures that the JavaScript code runs only after the entire HTML document has been loaded and parsed.
*   **API Key Management:**
    *   The `loadApiKey()` function retrieves the API key from `localStorage` using the `GEMINI_API_KEY_STORAGE_KEY`.
    *   The `saveApiKey()` function stores the API key from the input field into `localStorage`.
    *   The `updateApiStatus()` function visually indicates whether an API key is set and enables/disables the chat input and send button accordingly.
*   **Chat Interface Management:**
    *   `addMessage(sender, text)` dynamically creates and appends chat bubbles (`user` or `bot`) to the `#chat-messages` container. It also handles auto-scrolling to the latest message.
    *   `showTypingIndicator()` and `hideTypingIndicator()` manage the visibility of the "AI is typing..." message during API calls.
*   **Gemini API Interaction (`handleSendMessage` function):**
    *   When the user sends a message, their message is immediately displayed in the chat.
    *   The input field and send button are temporarily disabled to prevent multiple submissions, and the typing indicator is shown.
    *   A `fetch` POST request is made to the `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent` endpoint. The API key is appended as a query parameter.
    *   The request body is a JSON object formatted according to the Gemini API specifications, including the user's message in the `contents` array.
    *   Upon receiving a successful response, the code parses the AI's reply from `data.candidates[0].content.parts[0].text`.
    *   The bot's response is then displayed in the chat.
    *   **Error Handling:** A `try-catch` block is used to gracefully handle potential network errors or API-specific errors (e.g., invalid API key, rate limits). Error messages are displayed to the user.
    *   Finally, the typing indicator is hidden, and the input field and send button are re-enabled.

## License
This project is licensed under the MIT License. You are free to use, modify, and distribute this code for any purpose, provided that the original license notice is included.

## Contact
For any questions or feedback, please contact [Your Name/Email/GitHub Profile].