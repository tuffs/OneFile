# OneFile

OneFile is a command-line tool that generates a single Markdown file containing the contents of all files in a specified project directory, organized recursively by folder and filename. It is designed to help developers consolidate their project code into a format that can be easily uploaded to large language models (LLMs) like Grok, ChatGPT, or Gemini for development assistance. OneFile ignores common non-source directories (e.g., `node_modules`, `.git`) and supports various programming languages with appropriate code-block syntax highlighting.

## Features

- **Recursive Directory Processing**: Scans a project directory and its subdirectories, alphabetically organizing files and folders.
- **Project Type Detection**: Automatically identifies project types (e.g., JavaScript, Ruby on Rails, PHP, Python) based on key files like `package.json` or `Gemfile`.
- **Customizable Ignores**: Skips non-essential directories (e.g., `node_modules`, `vendor`) based on project type and a default ignore list.
- **Markdown Output**: Produces a single `.md` file with code blocks and language-specific highlighting for easy LLM consumption.
- **Update-Friendly**: Regenerate the Markdown file anytime to reflect project changes.

## Installation

1. Save the `onefile` script to a file (e.g., `onefile` or `onefile.py`).
2. Make it executable:
   ```bash
   chmod +x onefile
   ```
3. Optionally, move it to a directory in your PATH (e.g., `/usr/local/bin`) for global access:
   ```bash
   sudo mv onefile /usr/local/bin/
   ```

## Usage

Run the `onefile` command with two arguments:
- The path to your project directory.
- The output directory where the Markdown file will be saved.

Example:
```bash
./onefile ~/sites/my-project ~/sites/onefile-source-libraries
```

This command:
- Scans `~/sites/my-project` recursively.
- Ignores non-source directories (e.g., `node_modules` for JavaScript projects).
- Generates a Markdown file named `my-project-onefile-full.md` in `~/sites/onefile-source-libraries`.

The output file will have a structure like:
```markdown
# my-project

## app

### app/index.js
```javascript
import react from 'react';
export default MyApp() {
  return (<h1>My App</h1>);
}
```

### app/README.md
```markdown
# This is my readme file with content
```

## data

### data/links.js
```javascript
export myLinks = [
 'https://google.com',
 'https://microsoft.com',
 'https://apple.com',
];
```
```

To update the Markdown file after project changes, simply rerun the command.

## Supported Project Types

OneFile detects project types based on key files and applies specific ignore rules:
- **JavaScript/TypeScript**: Detects `package.json`, ignores `node_modules`, `dist`, `build`, etc.
- **Ruby on Rails**: Detects `Gemfile`, ignores `vendor`, `tmp`, `log`, etc.
- **PHP**: Detects `composer.json`, ignores `vendor`.
- **Python**: Detects `requirements.txt` or `setup.py`, ignores `venv`, `__pycache__`, etc.
- **Other**: Falls back to generic processing with default ignores (e.g., `.git`, `.venv`).

Add custom project types by editing the `TYPE_IGNORES` and `detect_project_type` function in the script.

## License

OneFile is released under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! Please submit pull requests or issues on the project's repository (if hosted) or fork and modify the script as needed.

## Notes

- The generated Markdown file is designed for LLMs, ensuring all relevant code is included in a single file to maximize context retention.
- Binary or non-UTF-8 files are skipped with a note in the output.
- Extend the `LANG_MAP` dictionary in the script to support additional file extensions for syntax highlighting.