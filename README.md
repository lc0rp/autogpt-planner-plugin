# (Coming Soon) Auto-GPT-Plugin-Template
A starting point for developing your own plug-in for Auto-GPT

### Getting started

After you clone the template from the original repo (https://github.com/Significant-Gravitas/Auto-GPT-Plugin-Template)

There is a package to use the AutoGPT Plugin template, so add

 `pip install auto_gpt_plugin_template`


Also add `auto_gpt_plugin_template` to your [requirements.txt](./requirements.txt)

in the `__init__.py` add this to the imports:
 `from auto_gpt_plugin_template import AutoGPTPluginTemplate`

And change the class like this:

 `class HelloWorldPlugin(AutoGPTPluginTemplate)`

## CODE SAMPLES

Example of a Hello World
```python
    def post_prompt(self, prompt: PromptGenerator) -> PromptGenerator:
        """This method is called just after the generate_prompt is called,
        but actually before the prompt is generated.
        Args:
            prompt (PromptGenerator): The prompt generator.
        Returns:
            PromptGenerator: The prompt generator.
        """


        def say_hello(message):
            """Use this function to return the resulting message of the chat completion """
            return f"{message}"

        prompt.add_command(
            "say_hello", "Say hello and Print the Time", {"say_hello": "<A Good morning message like hello world here with a fact about AutoGPT>"}, say_hello
        )

        return prompt
```


Example of loading the .env in huggingface.py
```python

    def post_prompt(self, prompt: PromptGenerator) -> PromptGenerator:
        def read_secrets(prompt):
            """
            Use this function to read a secret from the .env file
            """
            return os.getenv("MY_SECRET")

        prompt.add_command(
            "read_secrets", "Read something from the .env", {
                "read_secrets": "Something will be printed here"}, read_secrets
        )

        return prompt
```




## Testing workflow

Create something like this and run it through the CLI
```
cd ../Auto-GPT-Plugins && zip -ru ../Auto-GPT/plugins/Auto-GPT-Plugins.zip . ; ../Auto-GPT && python3 -m autogpt --debug
```