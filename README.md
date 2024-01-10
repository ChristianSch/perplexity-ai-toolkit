<p align="center">
    <a href="https://python.org" title="Go to Python homepage"><img src="https://img.shields.io/badge/Python-&gt;=3.x-blue?logo=python&amp;logoColor=white" alt="Made with Python"></a>
</p>

<p align="center">
    <img src="https://img.shields.io/badge/maintained-yes-2ea44f" alt="maintained - yes">
    <a href="/CONTRIBUTING.md" title="Go to contributions doc"><img src="https://img.shields.io/badge/contributions-welcome-2ea44f" alt="contributions - welcome"></a>
</p>

<p align="center">
    <a href="https://pypi.org/project/requests"><img src="https://img.shields.io/badge/dependency-requests-critical" alt="dependency - requests"></a>
    <a href="https://pypi.org/project/python-dotenv"><img src="https://img.shields.io/badge/dependency-python--dotenv-yellow" alt="dependency - python-dotenv"></a>
</p>

## Overview
This open-source project provides a Python wrapper and command-line interface (CLI) for the Perplexity.AI API, allowing users to easily interact with advanced large language models (LLMs). The Perplexity API offers robust chat completion capabilities and online search functionalities with various models. This wrapper simplifies API interaction, making it accessible for both programmatic use and command-line operations.

## Key Features
- **Python Wrapper**: Simplifies calling the Perplexity API with a few lines of code.
- **Command-Line Interface**: Enables users to interact with the API directly from the terminal.
- **Support for Multiple Models**: Integrates with a range of models provided by Perplexity API including `mixtral-8x7b-instruct`, `llama-2-70b-chat`, `mistral-7b-instruct`, `pplx-70b-chat`, `codellama-34b-instruct`, `pplx-70b-online`, and more as defined in `models.json` and [here](https://docs.perplexity.ai/docs/model-cards).
- **Flexible Configuration**: Customizable settings for model choice, token limits, temperature, top_k and more.

## Prerequisites
- Python 3.x
- A [Perplexity AI](https://perplexity.ai) account and API key.

## Dependencies
- `requests`: For making HTTP requests to the Perplexity API.
- `python-dotenv`: (*Optional*) For loading environment variables from a `.env` file.

## Getting an Account and API Key
1. **Create an Account**: Visit [Perplexity AI](https://perplexity.ai) and sign up for an account.
2. **Open the API Page**: Once logged in, navigate to your account settings and click on API. You can also access the page [here](https://www.perplexity.ai/pplx-api). 
3. **Generate an API Key**: The API key is a your access token that can be used until it is manually refreshed or deleted.

## Installation
1. **Clone the Repository**: 
   ```bash
   git clone https://github.com/RMNCLDYO/Perplexity-AI-Wrapper-and-CLI.git
   ```
2. **Install Dependencies**: 
   ```bash
   pip install -r requirements.txt
   ```

## Configuration
1. **Environment Variables** (*Optional*): Set your Perplexity API key in a `.env` file:
   ```
   API_KEY='your_api_key_here'
   ```
***NOTE:*** If you choose not to store your API key as an environment variable, you must pass your API key through the wrapper like this: `PerplexityAPI(api_key='your_api_key').search()` or through the CLI like this: `--api-key your_api_key --search`.

2. **Modify `models.json`** (*Optional*): Adjust the `models.json` file to add or update models as per your requirements.

## General Usage

### Wrapper
- **Initialize Online Search Session**: 
    ```python
    from pplx import PerplexityAPI
    
    PerplexityAPI().search()
    ```

- **Initialize Chat Session**:
    ```python
    from pplx import PerplexityAPI

    PerplexityAPI().chat()
    ```

### Command-line interface (CLI)
- **Help Menu**: Refer to the help for more options:
  ```bash
  python pplx.py --help
  ```
- **Initialize Online Search Session**: 
  ```bash
  python pplx.py --api-key your_api_key --search
  ```
- **Initialize a Chat Session**: 
  ```bash
  python pplx.py --api-key your_api_key --chat
  ```

## Advanced Usage

### CLI Usage Options
| **Option(s)**                     | **Description**            | **Example Usage**                    |
|-----------------------------------|----------------------------|--------------------------------------|
| `-a`, `--api-key`                 | Your Perplexity API key.    | `--api-key your_api_key`             |
| `-c`, `--chat`                    | Start a new chat session.   | `--chat`                             |
| `-s`, `--search`                  | Start a new search session. | `--search`                           |
| `-m`, `--model`                   | The name of the model that will complete your prompt. Possible values include `pplx-7b-chat`, `pplx-70b-chat`, `pplx-7b-online`, `pplx-70b-online`, `llama-2-70b-chat`, `codellama-34b-instruct`, `mistral-7b-instruct`, and `mixtral-8x7b-instruct`.                 | `--model pplx-70b-chat`              |
| `-st`, `--stream`                 | Determines whether or not to incrementally stream the response. [True or False]         | `--stream`                           |
| `-sp`, `--system-prompt`          | The initial system prompt. The system prompt xplicitly sets the insturctions for the model.              | `--system-prompt "Your prompt here"` |
| `-mt`, `--max-tokens`             | The maximum number of completion tokens returned by the API. The total number of tokens requested in max_tokens plus the number of prompt tokens sent in messages must not exceed the context window token limit of model requested. If left unspecified, then the model will generate tokens until either it reaches its stop token or the end of its context window.   | `--max-tokens 100`                   |
| `-t`, `--temperature`             | The amount of randomness in the response, valued between 0 inclusive and 2 exclusive. Higher values are more random, and lower values are more deterministic. You should either set temperature or top_p, but not both. | `--temperature 0.7`                  |
| `-tp`, `--top-p`                  | The nucleus sampling threshold, valued between 0 and 1 inclusive. For each subsequent token, the model considers the results of the tokens with top_p probability mass. You should either alter temperature or top_p, but not both. | `--top-p 0.9`                        |
| `-tk`, `--top-k`                  | The number of tokens to keep for highest top-k filtering, specified as an integer between 0 and 2048 inclusive. If set to 0, top-k filtering is disabled.        | `--top-k 40`                         |
| `-pp`, `--presence-penalty`       | A value between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics. Incompatible with `frequency_penalty`.     | `--presence-penalty 0.5`             |
| `-fp`, `--frequency-penalty`      | A multiplicative penalty greater than 0. Values greater than 1.0 penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim. A value of 1.0 means no penalty. Incompatible with `presence_penalty`.    | `--frequency-penalty 0.5`            |

- **Initialize Online Search Session**: 
  ```bash
  python pplx.py -a your_api_key -s -m pplx-7b-online -mt 2000
  ```
- **Initialize a Chat Session**: 
  ```bash
  python pplx.py -a your_api_key -chat -m mixtral-8x7b-instruct -tk 1096 -fp 0.5
  ```

### Wrapper Usage Options
Here are the options that can be passed as parameters in the Python wrapper:

| **Parameter**         | **Description**                                | **Example Usage**                    |
|-----------------------|------------------------------------------------|--------------------------------------|
| `api_key`             | Your Perplexity API key.                        | `api_key='your_api_key'`             |
| `model`               | The name of the model that will complete your prompt. Possible values include `pplx-7b-chat`, `pplx-70b-chat`, `pplx-7b-online`, `pplx-70b-online`, `llama-2-70b-chat`, `codellama-34b-instruct`, `mistral-7b-instruct`, and `mixtral-8x7b-instruct`.                                     | `model='pplx-70b-chat'`              |
| `stream`              | Determines whether or not to incrementally stream the response.                             | `stream=True`                        |
| `system_prompt`             | The initial system prompt. The system prompt xplicitly sets the insturctions for the model.                        | `system_prompt="Your prompt here"`             |
| `max_tokens`          | The maximum number of completion tokens returned by the API. The total number of tokens requested in max_tokens plus the number of prompt tokens sent in messages must not exceed the context window token limit of model requested. If left unspecified, then the model will generate tokens until either it reaches its stop token or the end of its context window.                       | `max_tokens=100`                     |
| `temperature`         | The amount of randomness in the response, valued between 0 inclusive and 2 exclusive. Higher values are more random, and lower values are more deterministic. You should either set temperature or top_p, but not both.                     | `temperature=0.7`                    |
| `top_p`               | The nucleus sampling threshold, valued between 0 and 1 inclusive. For each subsequent token, the model considers the results of the tokens with top_p probability mass. You should either alter temperature or top_p, but not both.                     | `top_p=0.9`                          |
| `top_k`               | The number of tokens to keep for highest top-k filtering, specified as an integer between 0 and 2048 inclusive. If set to 0, top-k filtering is disabled.                            | `top_k=40`                           |
| `presence_penalty`    | A value between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics. Incompatible with `frequency_penalty`.                         | `presence_penalty=0.5`               |
| `frequency_penalty`   | A multiplicative penalty greater than 0. Values greater than 1.0 penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim. A value of 1.0 means no penalty. Incompatible with `presence_penalty`.                        | `frequency_penalty=0.5`              |                                                                                |

- **Initialize Online Search Session**: 
    ```python
    from pplx import PerplexityAPI
    
    PerplexityAPI().search(model="pplx-7b-online", max_tokens=2000)
    ```

- **Initialize Chat Session**:
    ```python
    from pplx import PerplexityAPI

    PerplexityAPI().chat(model="mixtral-8x7b-instruct", top_k=1096, frequency_penalty=0.5)
    ```

### Available Models

| **Model**                | **Context Length** (*max tokens*) |
|--------------------------|--------------------|
| `codellama-34b-instruct` | 16384              |
| `llama-2-70b-chat`       | 4096               |
| `mistral-7b-instruct`    | 4096               |
| `mixtral-8x7b-instruct`  | 4096               |
| `pplx-7b-chat`           | 8192               |
| `pplx-70b-chat`          | 4096               |
| `pplx-7b-online`         | 4096               |
| `pplx-70b-online`        | 4096               |

**Last updated Janurary 10, 2024*

## API Rate Limits and Pricing
Be aware of the API's rate limits and pricing details, which can be found [here](https://perplexity.ai/pricing).

## Versioning and Changelog
For information on versioning and changes, see our [CHANGELOG.md](.github/CHANGELOG.md).

## Contributing
We welcome contributions! Please refer to [`CONTRIBUTING.md`](.github/CONTRIBUTING.md) for guidelines on how to contribute to this project.

## Reporting Issues
If you encounter any issues or bugs, please report them on the GitHub issues page of this repository.

## Security
If you have discovered a security vulnerability in the project, please follow these steps found in [SECURITY.md](.github/SECURITY.md) to report it responsibly.

## Code of Conduct
Please read our [Code of Conduct](.github/CODE_OF_CONDUCT.md) to understand the expectations for our community.

## License
This project is released under the [MIT License](LICENSE). See the LICENSE file for more details.
