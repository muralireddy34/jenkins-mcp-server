# Jenkins Server MCP

A Model Context Protocol (MCP) server that provides tools for interacting with Jenkins CI/CD servers. This server enables AI assistants to check build statuses, trigger builds, and retrieve build logs through a standardized interface.

## Installation

1. Clone this repository:
```bash
git clone https://github.com/iamishaan24/jenkins-mcp-server.git
cd jenkins-mcp-server
```

2. Install dependencies:
```bash
npm install
```

3. Build the project:
```bash
npm run build
```

## Configuration

The server requires the following environment variables:

- `JENKINS_URL`: The URL of your Jenkins server
- `JENKINS_USER`: Jenkins username for authentication
- `JENKINS_TOKEN`: Jenkins API token for authentication

Configure these in your MCP settings file:

### For Claude Desktop

MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "jenkins-server": {
      "command": "node",
      "args": ["/path/to/jenkins-server-mcp/build/index.js"],
      "env": {
        "JENKINS_URL": "https://your-jenkins-server.com",
        "JENKINS_USER": "your-username",
        "JENKINS_TOKEN": "your-api-token"
      }
    }
  }
}
```

## Tools and Usage





### 1. get_build_status

Retrieves the current status of a Jenkins build, including whether it is running, the result, timestamps, duration, and build URL. Supports fetching the latest build by default.

### 2. list_all_jobs

Lists all Jenkins jobs available on the server along with their job name, job URL, last build number, last build result, and Jenkins status color (blue, red, yellow, disabled, etc.).

### 3. list_recent_failed_jobs

Returns a list of Jenkins jobs whose most recent build failed. The results are sorted by the most recent failure time and can be limited to a specific number of jobs.

### 4. count_failed_jobs

Counts how many Jenkins jobs currently have their last build in a FAILURE state. Useful for quick health checks of the Jenkins instance.

### 5. get_failed_build_log

Fetches the console output of the last failed build for a specified Jenkins job. If no failed builds exist, the tool reports that clearly.

### 6. trigger_build

Triggers a new Jenkins build for a given job.

  * Uses /build for jobs without parameters.

  * Uses /buildWithParameters when parameters are provided.
    Automatically handles Jenkins CSRF (crumb) protection.

### 7. get_build_log

Retrieves the full console output of a specific Jenkins build, including support for fetching logs from the latest build.

### 8. create_jenkins_user

Creates a new Jenkins user in the internal Jenkins user database. This operation requires administrative permissions and supports setting username, password, full name, and email.

## Development

For development with auto-rebuild:
```bash
npm run watch
```

### Debugging

Since MCP servers communicate over stdio, you can use the MCP Inspector for debugging:

```bash
npm run inspector
```

This will provide a URL to access debugging tools in your browser.

## Thanks

Thanks AIMCP(https://www.aimcp.info).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
