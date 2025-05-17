## Text 2 Video Workflow

We will create text 2 video workflow here

In short goign direclty from text to videos is hard, it hard to control each aspect of the video and to ensure consistency in videos and what fidelity with what we want, we will approach it as two step problem
1. Create Discription of video what we want to AI. (Discription of video and how long it should be). It will generate a detail plan. Iterate over this plan to make sure you are satisfied with the plan and details of objects.
2. Use VLM ideally native text image model like geminin flash thinking to generate key points of the videos. 
3. Use keyframes/text to Video model to join short videos based on either one key frame or ideally two key frames describing end and start of short video clips
4. Get all the clips and join them.
5. Add audio to those clips, this will be added here in the future right now you can join the videos and add free audio from youtube or from speech to text models.
6. [Optionally] add subtitles to Video

we will demonstrate this workflow to create youtube shorts. shorts are right candidate for this workflow since text/Image to video models can only generate videos of small duration in high quality due to high computational requirements and in turn cost. We will be using replicate to use I/T 2 Video models for now but we can expand this to out serving or some other servings of these models.
Let's begin!
