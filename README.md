# Claude-to-OpenAI API Proxy: A Seamless Integration Solution

![Claude Proxy](https://img.shields.io/badge/Claude%20Proxy-v1.0.0-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Deployment](https://img.shields.io/badge/Deploy%20to%20Cloudflare%20Workers-Deploy-orange.svg)

## Overview

This repository contains a TypeScript project that acts as a proxy server deployed on Cloudflare Workers. It converts requests formatted for the [Claude API](https://docs.anthropic.com/claude/reference/messages_post) into the format required by the [OpenAI API](https://platform.openai.com/docs/api-reference/chat/create). This functionality allows any client compatible with the Claude API, such as the [Claude Code CLI](https://www.npmjs.com/package/@anthropic-ai/claude-code), to communicate with services that support the OpenAI API format.

For quick access to the latest releases, visit the [Releases section](https://github.com/DavidLabrin/claude_proxy/releases).

## Features

- **Dynamic Routing**: Route requests to any OpenAI-compatible API endpoint without modifying the code. You can specify the target API address and model name directly in the request URL.
  
- **Claude API Compatibility**: Full support for the `/v1/messages` endpoint, including both streaming and non-streaming responses.

- **Tool Calling Conversion**: Automatically convert Claude's `tools` format to OpenAI's format, ensuring compatibility with strict APIs like Google Gemini by cleaning the `input_schema`.

- **Haiku Model Shortcuts**: Pre-configured fixed routes for specific "Haiku" models through environment variables for quick access.

- **Easy Configuration Script**: The `claude_proxy.sh` script simplifies the setup process for users to configure their local Claude Code CLI to use this proxy.

- **Simple Deployment**: One-click deployment to the global Cloudflare Workers network.

## Getting Started

If you prefer not to deploy the proxy yourself, you can use the pre-configured public proxy service included in the script. This is the easiest and quickest way to get started.

### Step 1: Open the Configuration Script

Open the `claude_proxy.sh` file in your code editor.

### Step 2: Modify Variables

Locate the section labeled "Important: Replace the following content" and modify the following three variables according to your needs:

- `API_KEY`: **Your target service API key**.

### Step 3: Run the Script

After editing the script, run it to set up your local environment.

### Example Usage

Once configured, you can send requests to the proxy. Here’s a simple example of how to do this:

```bash
curl -X POST 'https://your-proxy-url.com/v1/messages' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer YOUR_API_KEY' \
-d '{
  "messages": [{"role": "user", "content": "Hello, Claude!"}]
}'
```

This request will be routed to the appropriate OpenAI API endpoint.

## Installation

To install the project locally, follow these steps:

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/DavidLabrin/claude_proxy.git
   cd claude_proxy
   ```

2. **Install Dependencies**:

   Make sure you have Node.js and npm installed. Then run:

   ```bash
   npm install
   ```

3. **Deploy to Cloudflare Workers**:

   You can deploy the project to Cloudflare Workers using the following command:

   ```bash
   npx wrangler publish
   ```

## Configuration

The configuration script allows you to set up your environment easily. The script has comments to guide you through the process. Make sure to replace the placeholder values with your actual API keys and endpoints.

### Environment Variables

The following environment variables are used in the project:

- `API_KEY`: Your API key for the target service.
- `HAIKU_MODEL`: The model you want to use for the Haiku shortcuts.

## API Endpoints

The proxy supports the following API endpoints:

- `POST /v1/messages`: Send messages to the OpenAI API. This endpoint supports both streaming and non-streaming responses.

### Request Format

The request format for the proxy is as follows:

```json
{
  "messages": [
    {
      "role": "user",
      "content": "Your message here."
    }
  ]
}
```

### Response Format

The response from the OpenAI API will be returned in the following format:

```json
{
  "id": "chatcmpl-abc123",
  "object": "chat.completion",
  "created": 1630000000,
  "model": "gpt-3.5-turbo",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Response from the assistant."
      },
      "finish_reason": "stop"
    }
  ]
}
```

## Troubleshooting

If you encounter issues while using the proxy, consider the following steps:

- **Check API Keys**: Ensure that your API keys are correct and have the necessary permissions.

- **Review Logs**: Check the logs in your Cloudflare Workers dashboard for any error messages.

- **Network Issues**: Verify your network connection and ensure that your requests are reaching the proxy.

## Contribution

Contributions are welcome! If you would like to contribute to this project, please follow these steps:

1. **Fork the Repository**: Click on the "Fork" button in the top right corner of the repository page.

2. **Create a New Branch**: 

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**: Implement your feature or fix.

4. **Commit Your Changes**:

   ```bash
   git commit -m "Add your message here"
   ```

5. **Push to Your Fork**:

   ```bash
   git push origin feature/your-feature-name
   ```

6. **Open a Pull Request**: Go to the original repository and click on "New Pull Request".

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For any questions or suggestions, feel free to open an issue in the repository or contact the maintainers.

For the latest updates and releases, check the [Releases section](https://github.com/DavidLabrin/claude_proxy/releases).

## Acknowledgments

- Thanks to the contributors and users for their support and feedback.
- Special thanks to the developers of Claude and OpenAI APIs for their innovative work.

## Future Enhancements

We plan to add more features and improvements to this project. Some ideas include:

- Enhanced error handling for better debugging.
- Support for additional OpenAI models.
- A user-friendly web interface for easier configuration and usage.

Stay tuned for updates!

## Conclusion

This project aims to bridge the gap between Claude and OpenAI APIs, providing a seamless integration experience. Whether you are a developer looking to utilize both APIs or just curious about the technology, this proxy server can simplify your tasks.