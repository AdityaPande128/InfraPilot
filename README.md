# InfraPilot - Agentic Devops Copilot for VS Code

**InfraPilot** is a seamless Visual Studio Code extension designed for developers and DevOps engineers to automatically generate least-privilege AWS IAM policies directly from their application code. 

By observing your code as you write, InfraPilot acts as an intelligent sidekick: the moment you save a file containing cloud service SDK usage (such as `boto3`), it steps in, analyzes your cloud activity, and dynamically generates the exact, minimal Terraform IAM policies required to securely execute your code.

##   Key Features

*   **Real-time Code Analysis**: Instantly scans your Python (`.py`) and JavaScript (`.js`) files on save for popular cloud SDK keywords like `boto3`, `s3`, `dynamodb`, and `google.cloud`.
*   **Powered by Gemini AI**: Integrates effortlessly with the Google Gemini API to produce context-aware, highly-accurate `json` IAM policies with zero wildcard privileges.
*   **Interactive Sidebar**: Review, inspect, and approve AI-generated IAM policies directly in the dedicated "InfraPilot Activity" Webview sidebar.
*   **Automated Terraform Writing**: Upon approval, InfraPilot intelligently appends the generated `aws_iam_policy` block to your workspace's `main.tf` file, or automatically creates an `infrapilot_iam.tf` file if one does not exist.
*   **Secure API Key Storage**: Safely manages your Gemini API credentials via your operating system's native keychain using the `vscode.SecretStorage` API.

##   Usage Instructions

1.  **Set your API Key**:
    *   Open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows/Linux).
    *   Search for **`InfraPilot: Add / Set Gemini API Key`** and securely enter your Google Gemini API token.
2.  **Write Cloud Code**:
    *   Open a workspace containing your codebase.
    *   Write or modify a Python or JS script that interacts with cloud services.
    *   *Example*: `s3 = boto3.client('s3'); response = s3.list_buckets()`
3.  **Save Your File**:
    *   Hit `Cmd+S` (or `Ctrl+S`).
    *   InfraPilot will detect the cloud activity and automatically open the **InfraPilot Activity Sidebar** with a newly generated IAM policy for your review.
4.  **Approve**:
    *   Click **Approve & Append to Terraform** in the sidebar. InfraPilot will format and inject your new Terraform policy block straight into your current workspace!

##  Privacy & Security

*   **Least-Privilege Focus**: The internal AI prompt explicitly demands "least-privilege actions" and forbids wildcards (`*`).
*   **Native Keychain Encryption**: API keys are never stored in plaintext within the extension or your project; they reside safely in your OS keyring.
*   *(Note: This extension transmits file contents to Google's Generative AI endpoint for analysis upon save. Ensure your organization's data policies permit cloud-based code analysis.)*

##  Requirements

*   Visual Studio Code version `1.109.0` or higher.
*   An active internet connection.
*   A valid [Google AI Studio (Gemini) API Key](https://aistudio.google.com/).

##  Feedback & Contribution

This is an early release. Feedback, issues, and pull requests are highly encouraged to help InfraPilot better detect complex cloud patterns across more languages and frameworks!

---
*Created with love by Aditya Pande.*
