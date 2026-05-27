

# Ex.No.6 - Development of Python Code Compatible with Multiple AI Tools

## Aim

To write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights.

## Explanation

This experiment focuses on developing Python code that can interact with multiple AI tools through their APIs.

The program sends the same prompt to different AI tools, collects their responses, compares the outputs, and generates useful observations.

This helps users understand how to request help from AI tools for tasks such as:

- Writing Python code
- Integrating with APIs
- Comparing generated answers
- Producing actionable insights

In real-world applications, different AI tools may produce different responses for the same prompt. Some tools may provide more accurate answers, while others may provide deeper explanations or better structure.

A comparison program helps evaluate these responses systematically.


## Tools and Technologies Used

| Tool / Technology | Purpose |
|---|---|
| Python | Used as the programming language for API integration and response comparison. |
| Requests Library | Used to send HTTP POST requests to AI API endpoints. |
| OpenAI API | Used as one AI tool for generating responses. |
| Groq API | Used as another AI tool with OpenAI-compatible chat completion format. |
| Environment Variables | Used to store API keys securely without hard-coding them in the program. |


## Procedure

1. Select two or more AI tools that provide API access.
2. Create API keys for the selected tools and store them as environment variables.
3. Write a Python program that sends the same prompt to each AI tool.
4. Collect the generated responses from all AI tools.
5. Compare the responses using criteria such as accuracy, clarity, depth, and usefulness.
6. Generate actionable insights from the comparison.
7. Record the output and result of the experiment.



## System Design

The system uses a simple API comparison workflow.

First, the user defines a prompt. Next, the Python program sends the prompt to each configured AI tool. After receiving the responses, the program prints each output and calculates simple comparison details such as word count.

Finally, it gives guidelines for identifying the best response.

| Stage | Description |
|---|---|
| Input | A single prompt is provided by the user. |
| API Request | The same prompt is sent to multiple AI tool APIs. |
| Response Collection | The program stores the response from each AI tool. |
| Comparison | The responses are compared based on clarity, depth, accuracy, and usefulness. |
| Insight Generation | The program prints observations that help the user select the best output. |



## Python Code

```python
import os
import requests

AI_TOOLS = {
    "OpenAI": {
        "url": "https://api.openai.com/v1/chat/completions",
        "api_key": os.getenv("OPENAI_API_KEY"),
        "model": "gpt-4o-mini"
    },
    "Groq": {
        "url": "https://api.groq.com/openai/v1/chat/completions",
        "api_key": os.getenv("GROQ_API_KEY"),
        "model": "llama-3.1-8b-instant"
    }
}

def call_ai_tool(tool_name, prompt):
    tool = AI_TOOLS[tool_name]

    headers = {
        "Authorization": f"Bearer {tool['api_key']}",
        "Content-Type": "application/json"
    }

    data = {
        "model": tool["model"],
        "messages": [
            {"role": "system", "content": "You are a helpful AI assistant."},
            {"role": "user", "content": prompt}
        ],
        "temperature": 0.4
    }

    response = requests.post(
        tool["url"],
        headers=headers,
        json=data,
        timeout=30
    )

    response.raise_for_status()

    return response.json()["choices"][0]["message"]["content"]

def compare_outputs(outputs):
    print("\n--- AI Tool Output Comparison ---")

    for tool, output in outputs.items():
        print(f"\n{tool} Output:")
        print(output)
        print(f"Word Count: {len(output.split())}")

    print("\n--- Actionable Insights ---")
    print("1. Compare accuracy by checking whether the answer directly solves the task.")
    print("2. Compare depth by checking examples, explanation, and reasoning.")
    print("3. Compare clarity by checking structure, readability, and usefulness.")
    print("4. Select the output that is most accurate, complete, and practical.")

def main():
    prompt = "Explain how Python can be used to automate API comparison between AI tools."

    outputs = {}

    for tool_name in AI_TOOLS:
        try:
            outputs[tool_name] = call_ai_tool(tool_name, prompt)
        except Exception as error:
            outputs[tool_name] = f"Error while calling {tool_name}: {error}"

    compare_outputs(outputs)

if __name__ == "__main__":
    main()
```


## Code Explanation

| Code Section | Explanation |
|---|---|
| `AI_TOOLS` dictionary | Stores API endpoint, API key, and model name for each AI tool. |
| `call_ai_tool()` function | Sends the user prompt to the selected AI tool and returns the generated response. |
| `compare_outputs()` function | Displays each response, calculates word count, and prints comparison insights. |
| `main()` function | Controls the program flow by sending the prompt to all tools and comparing the outputs. |
| Exception handling | Prevents the program from stopping completely if one API call fails. |



## Sample Input Prompt

```text
Explain how Python can be used to automate API comparison between AI tools.
```



## Sample Output

```text
--- AI Tool Output Comparison ---

OpenAI Output:
Python can automate API comparison by sending the same prompt to different AI tools, collecting their responses, and comparing them based on accuracy, clarity, depth, and usefulness.
Word Count: 26

Groq Output:
Python can be used with HTTP request libraries to call multiple AI APIs. The program can store responses, calculate response length, check keywords, and generate a comparison report.
Word Count: 28

--- Actionable Insights ---
1. Compare accuracy by checking whether the answer directly solves the task.
2. Compare depth by checking examples, explanation, and reasoning.
3. Compare clarity by checking structure, readability, and usefulness.
4. Select the output that is most accurate, complete, and practical.
```


## Response Comparison

| Criteria | OpenAI Output | Groq Output | Observation |
|---|---|---|---|
| Clarity | Clear and direct explanation. | Clear with slightly more implementation detail. | Both outputs are understandable. |
| Accuracy | Correctly explains API comparison. | Correctly mentions HTTP requests and response storage. | Both are accurate for the given prompt. |
| Depth | Moderate depth with evaluation criteria. | More detailed about libraries and keyword checks. | Groq output is slightly deeper in implementation. |
| Usefulness | Useful for understanding the concept. | Useful for coding-oriented explanation. | Choice depends on whether the user wants concept or implementation. |



## Analysis

The Python program demonstrates how multiple AI tools can be accessed using API calls. The same input prompt is sent to each tool, which makes the comparison fair.

The outputs can then be evaluated using common criteria such as:

- Quality
- Accuracy
- Clarity
- Depth
- Usefulness

The experiment also shows the importance of API key management. API keys should not be written directly inside the source code because that can expose private credentials. Instead, environment variables are used to keep the keys secure.

The comparison does not automatically decide the best AI response in a fully intelligent way. However, it provides a useful foundation.

The program can be improved further by adding:

- Scoring methods
- Keyword matching
- Sentiment checks
- Response time measurement
- Cost comparison
- Automatic report generation


## Actionable Insights

- Use the same prompt for all AI tools to ensure a fair comparison.
- Check whether each response directly answers the question.
- Evaluate the response based on clarity, accuracy, depth, and usefulness.
- Use environment variables to protect API keys.
- Add scoring methods if the comparison needs to be automated further.
- Choose the AI tool based on the task, not only based on response length.

## Output

Python code was developed to interact with multiple AI tool APIs, collect responses, compare outputs, and generate actionable insights.

The sample output shows how responses from different AI tools can be compared using clarity, accuracy, depth, and usefulness.



## Result
Thus, Python code compatible with multiple AI tools was developed and explained.

The experiment demonstrates how APIs can be used to automate AI interaction, compare model responses, and generate useful insights for selecting the most suitable 
AI output.
