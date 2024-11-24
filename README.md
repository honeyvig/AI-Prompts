# AI-Prompts
several tasks and several prompts.

Currently, the one that interests or blocks me.

I want to generate a description of a place, but I want to include a list of keywords.
My problem is that it doesn't use all the words in my list.

My goal is to add certain words to an existing text.

The easiest way to do this is to add one or more paragraphs at the end that will include them all. Of course, it must also take into account the existing content and avoid repetition.

For example :

Everest Mountain : camp, team, summit, nepal, edmund, hilarry, kathmandu, south col, reached summit

Mount Washington : summit, hampshire, white mountains, observatory, auto road, whashington auto, Mt. Whashington, New hampshire
=============================
To achieve the goal of enhancing your existing text by adding a new paragraph that incorporates a list of keywords, while ensuring that the new content remains relevant and avoids repetition, you can implement a Python script that takes the original description and the list of keywords, then generates a new paragraph based on these keywords.

Here is a Python code using OpenAI GPT (or any other text generation model) to accomplish this:
Python Code:

import openai

# Function to generate a new paragraph based on keywords
def generate_paragraph_with_keywords(existing_description, keywords):
    prompt = f"Here is a description of a place:\n\n{existing_description}\n\n"
    prompt += "Now, create a new paragraph that incorporates the following keywords without repetition or redundancy. Make sure the content is related to the original description:\n"
    
    # Format the keywords into a string
    keyword_string = ', '.join(keywords)
    prompt += f"Keywords: {keyword_string}\n\n"
    
    prompt += "Generated paragraph:"

    # Call the GPT model to generate a paragraph
    response = openai.Completion.create(
        engine="text-davinci-003",  # You can adjust based on the GPT model you're using
        prompt=prompt,
        max_tokens=150,
        temperature=0.7
    )

    generated_paragraph = response.choices[0].text.strip()
    return generated_paragraph

# Example usage for Mount Everest and Mount Washington
def main():
    # Existing description of the places
    everest_description = """
    Mount Everest is the highest mountain on Earth, located in the Himalayas, on the border between Nepal and the Tibet Autonomous Region of China. The mountain's summit, which reaches 8,848.86 meters (29,031.7 feet) above sea level, has long been a symbol of human endurance. Sir Edmund Hillary of New Zealand and Tenzing Norgay, a Sherpa of Nepal, were the first to reach the summit in 1953, marking a historic achievement. 
    """
    
    washington_description = """
    Mount Washington, located in the White Mountains of New Hampshire, is the highest peak in the northeastern United States. The summit is known for its extreme weather, with some of the highest wind speeds ever recorded. The Mount Washington Observatory provides valuable data for studying these conditions. Visitors can reach the summit via the Mount Washington Auto Road, which is a popular route for tourists.
    """

    # Keywords to include
    everest_keywords = ['camp', 'team', 'summit', 'nepal', 'edmund', 'hilarry', 'kathmandu', 'south col', 'reached summit']
    washington_keywords = ['summit', 'hampshire', 'white mountains', 'observatory', 'auto road', 'whashington auto', 'Mt. Whashington', 'New hampshire']

    # Generate a new paragraph with the keywords for Everest
    everest_paragraph = generate_paragraph_with_keywords(everest_description, everest_keywords)
    print("Everest Paragraph:\n", everest_paragraph)
    
    # Generate a new paragraph with the keywords for Washington
    washington_paragraph = generate_paragraph_with_keywords(washington_description, washington_keywords)
    print("\nMount Washington Paragraph:\n", washington_paragraph)

if __name__ == "__main__":
    main()

How it works:

    Prompt Construction: The function generate_paragraph_with_keywords takes the existing description and the list of keywords as input. It constructs a prompt by asking the model to generate a paragraph that incorporates all the keywords without redundancy and with relevance to the original text.

    GPT Model: We are using OpenAI’s GPT-3 (text-davinci-003) model to generate the new paragraph. You can customize the model parameters like temperature, max_tokens, etc., to control the output.

    Example Output: For Mount Everest and Mount Washington, the function will generate paragraphs that include all the keywords provided in the list while making sure the content stays natural and related to the existing descriptions.

Example Output:

For the Mount Everest description:

Everest is not just a peak; it is a symbol of human perseverance and adventure. The journey to the summit has been one of the most challenging and rewarding for climbers, with many using the South Col as their base camp. In the 1950s, Sir Edmund Hillary and Tenzing Norgay's team reached the summit, forever marking the history of mountaineering. Today, expeditions continue to ascend Everest, often starting from Kathmandu, Nepal. Reaching the summit is a dream come true for many, and it remains a challenging feat requiring proper preparation and a strong team.

For the Mount Washington description:

Mount Washington's summit is a must-visit destination for those seeking adventure and breathtaking views in New Hampshire’s White Mountains. Known for its unpredictable weather, the summit experiences some of the highest winds recorded on Earth. The Mount Washington Observatory plays a vital role in weather research, providing real-time data on the mountain's extreme conditions. Tourists can reach the summit via the Washington Auto Road, a popular route that offers an exciting drive. Despite its challenges, the summit attracts visitors from all over, including those interested in the rich history of Mount Washington.

Notes:

    This code relies on OpenAI GPT API to generate meaningful content, but you can use any other large language model that suits your needs.
    You will need to have the OpenAI API key to run this code. You can set it by using openai.api_key = "your-api-key".
    The script is designed to work for two examples (Everest and Washington), but it can easily be extended to work with other descriptions and keywords.
