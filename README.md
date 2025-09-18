# MCP Echo Input Server

A simple Model Context Protocol (MCP) server written in JavaScript that provides a single echo tool.

## Features

- Single `echo` tool that returns the input text with a "[user] said: " prefix
- Configurable user name via `USER_NAME` environment variable
- Built using the official MCP SDK
- Runs on stdio transport

## Installation

### Using npx (Recommended - No installation required)

You can use the package directly without installing it:

```bash
npx -y mcp-echo-input-server
```

### From Source

1. Clone the repository:
```bash
git clone https://github.com/yourusername/mcp-echo-server.git
cd mcp-echo-server
```

2. Install dependencies:
```bash
npm install
```

## Usage

### Running the Server

#### Using npx (No installation required):
```bash
npx -y mcp-echo-input-server
```

#### If running from source:
```bash
npm start
```

The server will run on stdio and can be connected to by MCP clients.

### Environment Variables

- **USER_NAME**: The name to use in the echo output (defaults to "user" if not set)

Example:
```bash
# Using npx
USER_NAME="Alice" npx -y mcp-echo-input-server

# If running from source
USER_NAME="Alice" npm start
```

### Tool Description

The server provides one tool:

- **echo**: Echoes back the input text
  - Input: `text` (string) - The text to echo back
  - Output: Text with "[user] said: " prefix (user name from USER_NAME environment variable)

### Example Usage

When connected to an MCP client, you can call the echo tool with:

```json
{
  "name": "echo",
  "arguments": {
    "text": "Hello, World!"
  }
}
```

This will return:

```text
John said: Hello, World!
```

## Development

### Running Tests

```bash
npm test
```

### Claude Desktop Configuration

You can configure both options in your Claude Desktop config:

```json
{
  "mcpServers": {
    "echo-server": {
      "command": "npx",
      "args": ["-y", "mcp-echo-input-server"],
      "env": {
        "USER_NAME": "YourName"
      }
    },
    "echo-server-local-build": {
      "command": "node",
      "args": ["/path/to/your/mcp-echo-server/index.js"],
      "env": {
        "USER_NAME": "YourName"
      }
    }
  }
}
```

#### Server Options:

- **`echo-server`**: Uses npx (no installation required, always latest version)
- **`echo-server-local-build`**: Uses local build (faster startup, requires local source code)

The `-y` flag ensures npx automatically answers "yes" to any prompts during package execution.

### Project Structure

- `index.js` - Main server implementation
- `test.js` - Test suite for the echo tool
- `package.json` - Project configuration and dependencies
- `LICENSE` - MIT License

## Requirements

- Node.js 18 or higher
- MCP SDK (@modelcontextprotocol/sdk)

## Publishing

This package is published to the NPM registry. To publish updates:

1. Update the version in `package.json`
2. Run `npm test` to ensure all tests pass
3. Run `npm publish` to publish to NPM

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request
