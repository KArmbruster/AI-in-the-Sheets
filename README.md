# Google Sheets Gemini API Integration

A powerful and easy-to-use Google Apps Script that connects your Google Sheets to the Google Gemini API. This script allows you to leverage the power of generative AI directly within your spreadsheets through a simple custom function (`=GEMINI()`) and a user-friendly menu.
Process text, generate content, translate languages, summarize data, and much more, all without leaving your Google Sheet.

## Features

- **Custom Sheet Function**: Directly call the Gemini API from any cell with the `=GEMINI()` function.
- **Multi-Cell Prompts**: Concatenate text from multiple cells to form a single, powerful prompt (e.g., `=GEMINI(A2:C2)`).
- **Adjustable Creativity**: Control the randomness of the AI's response by setting a `temperature` parameter (defaults to `0.0` for deterministic output).
- **Secure API Key Storage**: Your API key is stored securely using Google's `PropertiesService`, not hardcoded in the script.
- **Simple Setup**: Get up and running in minutes with a simple copy-paste installation.

## Setup and Installation

Follow these steps to add the Gemini API functionality to your Google Sheet.

#### **Step 1: Open the Apps Script Editor**

1.  Open the Google Sheet you want to add the script to.
2.  Click on **Extensions** > **Apps Script**. This will open a new tab with the script editor.

#### **Step 2: Paste the Code**

1.  Delete any placeholder code in the `Code.gs` file.
2.  Copy the complete code from the `Code.gs` file in this repository and paste it into the script editor.
3.  Click the **Save project** icon (it looks like a floppy disk). You can give the project a name, like "Gemini Integration".

#### **Step 3: Get a Google Gemini API Key**

1.  Go to **[Google AI Studio](https://aistudio.google.com/)**.
2.  Sign in with your Google account.
3.  Click on **"Get API key"** and then **"Create API key in new project"**.
4.  Copy the generated API key. Keep this key safe and do not share it publicly.

#### **Step 4: Set the API Key in Your Sheet**

1.  Return to your Google Sheet. You may need to refresh the page.
2.  A new menu named **"Gemini AI"** should now appear in the menu bar.
3.  Click **Gemini AI** > **Set API Key**.
4.  In the prompt, paste the API key you obtained from Google AI Studio and click **OK**.

Your script is now installed and ready to use!

## Usage

You can interact with the Gemini API using the `=GEMINI()` custom function. This is the most flexible way to use the script, and you can use it just like any other spreadsheet function.

**Syntax:**


=GEMINI(prompt_range, [temperature])

Generated code
- **`prompt_range`**: The cell (e.g., `A2`) or range of cells (e.g., `A2:C2`) containing your prompt. If you provide a range, the text from all cells in that range will be joined together to form a single prompt.
- **`[temperature]`** (Optional): A number between `0.0` and `1.0` that controls the creativity of the AI.
    - `0.0`: The most deterministic and predictable output.
    - `1.0`: The most creative and random output.
    - **Default**: `0.0` if not specified.

**Examples:**

- **Simple prompt from one cell:**
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

=GEMINI(A2)

Generated code
- **Prompt combining multiple cells:**
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

=GEMINI(A2:C2)

Generated code
- **Prompt with a specific temperature for more creative output:**
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END

=GEMINI(A2, 0.7)

Generated code
## Configuration

### Model
The script is hardcoded to use the `gemini-2.5-flash-lite-preview-06-17` model, which is optimized for speed and cost-effectiveness. You can change this by editing the `model` variable in the `callGeminiAPI` function within the script.

### Error Handling
- If the API key is not set, the script will return an error message prompting you to set it via the menu.
- If the API call fails for any other reason (e.g., network issues, invalid prompt), an error message from the API will be displayed in the cell.

## Security
To protect your credentials, your Gemini API key is stored using Google Apps Script's `PropertiesService`. This service stores data on Google's servers and is scoped to the script, making it a secure alternative to hardcoding the key directly in the source code.

## License
This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
IGNORE_WHEN_COPYING_END
