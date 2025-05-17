# Plan this using reasoning model like grok2 or deepseek or chatgpt reasoning

prompt = "A 3D Image of a cartoon green dragon with red tounge"

# Generate the image
response = client.models.generate_content(
    model=model_id,
    contents=prompt,
    config=config
)


# Iterate over the response candidates and display the image and text
for part in response.candidates[0].content.parts:
    if part.inline_data:
        display_image(part.inline_data.data)
        save_image(part.inline_data.data, f"dragon.png")
    else:
        display(Markdown(part.text))


prompt = "Make the dragon breath fire"

# Generate the image
response = client.models.generate_content(
    model=model_id,
    contents=[prompt,PILImage.open("dragon.png")],
    config=config
)

for part in response.candidates[0].content.parts:
    if part.inline_data:
        display_image(part.inline_data.data)
        save_image(part.inline_data.data, f"dragon2.png")
    else:
        display(Markdown(part.text))
it produces these two dragon pictures now I want to create a funny video for children using them as start and end image of only 5 seconds but it needs to be funny for children I am planning to use replicate

start_image="dragon.png"
end_image="dragon2.png"
print(f"Start image exists? {os.path.exists(start_image)}, End image exists? {os.path.exists(end_image)}")
image_start = open("dragon.png", "rb")
image_end = open("dragon2.png", "rb")

can you fill the input promt of the model to make sure we acheive the objective 
input = {
    "prompt": "",
    "start_image": image_start,
    "end_image": image_end,
    "duration": 5,
    "cfg_scale": 0.5,
    "negative_prompt": 
} we are planning to use "kwaivgi/kling-v1.6-pro" model for this 

### Out from grok2 
input = {
    "prompt": "Create a 5-second animation featuring a cartoon green dragon with a red tongue. Begin with the dragon standing still, sticking its tongue out playfully (start image). Suddenly, it starts to dance in a silly way, shaking its plump belly like jelly and flapping its small wings like a clumsy bird. As it dances, it takes a deep breath, looking determined, but only a tiny puff of smoke comes out, making it pout with big, sad eyes. It tries again, puffing its cheeks comically, but another small puff escapes, causing it to slip and slide on its feet with a goofy tumble. Finally, it stands tall, takes a massive breath, its chest and belly inflating like a balloon, and breathes a huge burst of fire (end image), finishing with a proud, beaming smile.",
    "start_image": image_start,
    "end_image": image_end,
    "duration": 5,
    "cfg_scale": 0.5,
    "negative_prompt": "no scary elements, no dark themes, no realistic violence, no complex backgrounds, no dull colors"
}

## Adding voice to videos

Maybe use something like [Orpheus TTS](https://github.com/canopyai/Orpheus-TTS) to generate voice for videos probably need to finetune the model as it is mostly adults voices maybe need to finetune on cartoon or children voices.