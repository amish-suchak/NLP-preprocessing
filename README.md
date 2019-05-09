# Pre-processing in Natural Language Processing projects. 

The purpose of this repository is to understand the various pre-processing techniques applied to NLP tasks. We take a sample input dataset known as the [Myers-Briggs Personality Type Dataset](https://www.kaggle.com/datasnaek/mbti-type). The dataset is used to predict the personality of the user based on their social media posts. 

The input data is split into two columns: 

## Type

This is the personality type of the user as based on the MBTI classes. There are 4 different classifications based on personality type yielding a total of 16 different combinations. For each person, we ask:

•	Whether someone would prefer dealing with people directly and learn from their external environment (**Extraversion**) or if they would perceive, gain insights and obtain ideas internally (**Introversion**). 

•	Whether someone would want to deal with things that they would already know or feel from one of their senses (**Sensing**) or if they would want to trust what they believe is right even though they would not have experienced it for themselves (Intuition).

•	Whether someone would make a decision based on logical thinking and coming up with a conclusion (**Thinking**) or if they prefer making a decision based on their “gut” (**Feeling**). 

•	Whether someone would want everything planned out (**Judgment**) or just have no plan and make one along the way (**Perception**). 

## Posts

The posts are the 50 most recent things that users have posted on the PersonalityCafe forum. We can take a look at a sample of about 12 posts made by one user here: 

>'Dear INTP,   I enjoyed our conversation the other day.  Esoteric gabbing about the nature of the universe and the idea that every rule >and social code being arbitrary constructs created...|||Dear ENTJ sub,   Long time no see.  Sincerely, Alpha|||None of them. All other >types hurt in deep existential ways that I want no part of.|||Probably a sliding scale that depends on individual preferences, like >everything in humanity.|||Draco Malfoy also. I'd say he's either 358 or 368.|||I'm either 358 or 385, though in which stacking to me is >a somewhat arbitrary distinction to make as I believe that the core indicates primary motivation and has a hand in every action. >Therefore, a...|||I'm not particularly introverted or extraverted, personally. That said, I would say I'm somewhat unphased by either >social interactions or being alone. What I'd say I crave more so than anything is...|||Dear Type 9 INFP,  Your absolute admiration of >me is refreshing. You're a great girlfriend and I wish we both didn't have such busy schedules so we could be around one another more >often.  Keep...|||2% still means about 1/50 people. I've probably seen 1-2 others today. I never understood fascination by virtue of >rarity.|||So, you're on the ESFJ train also, right?|||I have toyed with the idea of the OP being an extrovert also for awhile now, >actually. After many conversations with him, however I'm disinclined to believe it due to OP being much too close with Fi...|||Still >ESFJ|||I disagree.  Definite ESFJ. Fe- Si ALL up in this.|||Where have you been?  Your mother and I have been worried sick.|||Similar >feelings concerning ENTPs.|||I collect shoes. I do so because I like status and nothing communicates such a thing as much as a pair of >Jordans.
