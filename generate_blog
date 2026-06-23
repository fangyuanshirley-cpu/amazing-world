# Generate a Blog with OpenAI 📝
# Modern version that runs today (OpenAI Python SDK v1.x).
#
# Setup:
#   pip install openai python-dotenv
#   Create a .env file next to this script containing:
#       API_KEY=sk-your-real-key-here
#
# Differences from the 2022 tutorial:
#   - openai.Completion.create  ->  client.chat.completions.create
#   - model 'text-davinci-002' (retired) -> 'gpt-4o-mini'
#   - response.choices[0].text  ->  response.choices[0].message.content

from openai import OpenAI
from dotenv import dotenv_values

config = dotenv_values('.env')

# The modern SDK uses a client object instead of a global api_key.
client = OpenAI(api_key=config['API_KEY'])


def generate_blog(paragraph_topic):
    response = client.chat.completions.create(
        model='gpt-4o-mini',
        messages=[
            {
                'role': 'user',
                'content': 'Write a paragraph about the following topic. ' + paragraph_topic,
            }
        ],
        max_tokens=400,
        temperature=0.3,
    )

    retrieve_blog = response.choices[0].message.content
    return retrieve_blog


keep_writing = True

while keep_writing:
    answer = input('Write a paragraph? Y for yes, anything else for no. ')
    if answer == 'Y':
        paragraph_topic = input('What should this paragraph talk about? ')
        print(generate_blog(paragraph_topic))
    else:
        keep_writing = False
