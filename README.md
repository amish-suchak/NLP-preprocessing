# Pre-processing in Natural Language Processing projects. 

## Dataset

The purpose of this repository is to understand the various pre-processing techniques applied to NLP tasks. We take a sample input dataset known as the [Myers-Briggs Personality Type Dataset](https://www.kaggle.com/datasnaek/mbti-type). The dataset is used to predict the personality of the user based on their social media posts. 

The input data is split into two columns: 

### Type

This is the personality type of the user as based on the MBTI classes. There are 4 different classifications based on personality type yielding a total of 16 different combinations. For each person, we ask:

•	Whether someone would prefer dealing with people directly and learn from their external environment (**Extraversion**) or if they would perceive, gain insights and obtain ideas internally (**Introversion**). 

•	Whether someone would want to deal with things that they would already know or feel from one of their senses (**Sensing**) or if they would want to trust what they believe is right even though they would not have experienced it for themselves (Intuition).

•	Whether someone would make a decision based on logical thinking and coming up with a conclusion (**Thinking**) or if they prefer making a decision based on their “gut” (**Feeling**). 

•	Whether someone would want everything planned out (**Judgment**) or just have no plan and make one along the way (**Perception**). 

### Posts

The posts are the 50 most recent things that users have posted on the PersonalityCafe forum. We can take a look at a sample: 

>'Dear INTP,   I enjoyed our conversation the other day.  Esoteric gabbing about the nature of the universe and the idea that every rule and social code being arbitrary constructs created...|||Dear ENTJ sub,   Long time no see.  Sincerely, Alpha|||None of them. All other types hurt in deep existential ways that I want no part of.|||Probably a sliding scale that depends on individual preferences, like everything in humanity.|||Draco Malfoy also. I'd say he's either 358 or 368.|||I'm either 358 or 385, though in which stacking to me is a somewhat arbitrary distinction to make as I believe that the core indicates primary motivation and has a hand in every action. Therefore, a...|||I'm not particularly introverted or extraverted, personally. That said, I would say I'm somewhat unphased by either social interactions or being alone. What I'd say I crave more so than anything is...|||Dear Type 9 INFP,  Your absolute admiration of me is refreshing. You're a great girlfriend and I wish we both didn't have such busy schedules so we could be around one another more often.  Keep...|||2% still means about 1/50 people. I've probably seen 1-2 others today. I never understood fascination by virtue of rarity.|||So, you're on the ESFJ train also, right?|||I have toyed with the idea of the OP being an extrovert also for awhile now, actually. After many conversations with him, however I'm disinclined to believe it due to OP being much too close with Fi...|||Still ESFJ|||I disagree.  Definite ESFJ. Fe- Si ALL up in this.|||Where have you been?  Your mother and I have been worried sick.|||Similar feelings concerning ENTPs.|||I collect shoes. I do so because I like status and nothing communicates such a thing as much as a pair of Jordans.

Each post is separated by 3 lines **|||** . We also see that there is a significant amount of pre-processing we can do to the data since we want to normalize the data as much as possible before we feed it into a model. We will cover all the various steps we would take in the next section. 


## Pre-processing

This step involves cleaning the data and performing some pre-processing such that we would be able to feed it into a Recurrent Neural Network based model. In the notebook, we will go through each phase of the pre-processing step and see what the output looks like for the same paragraph. In this section, we describe the steps we will take and why they are necessary. 

### Replacing links 
This step removes all the hyperlinks. For a deeper understanding of a problem, we can take the information such as video title from YouTube links or Image Captions from Images since they may provide some insights. 

### Removing symbols and numbers
This step removes all the symbols and numbers that we do not require. Depending on the problem, we can also replace the integer digits by the word if we would want to retain information about the numerical data. 

### Fixing word contractions
This changes the word contractions. Considering an informal forum, users would be more inclined to user abbreviations. For example, instead of saying "Oh my God", they would simply type "omg". Similarly, instead of typing "You are", users would type "you're".  We fix these contractions with the help of the contractions library on Python. 

### Lower-case 

This ensures that all the words are lower case. When we move over to the tokenizer stage, we want to make sure that the word "**S**ample" is treated the same as the word "**s**ample". 

### Removing stop-words 
Stop words do not contribute much to the overall semantic understanding of a sentence. Web searches also generally remove the stop words. Examples of these words include: 
> a, an, and , it, its, of, on, that, to

### Stemming and Lemmatization 

Stemming essentially shortens the word by cutting of the suffix. In this case, the word “cleaning” changes into the word “clean”. This helps standardize words so that “cleaning” and “clean” would be considered the same meaning. However, stemming does not usually work well as intended. There are words which would be stemmed out but mean something completely different after cutting the suffix. Therefore, another technique called “Lemmatization” was introduced. Lemmatization changes the word into the root word. For example, in lemmatization, the word “is” and “are” changes into the root word “be”. 

After this step, we can see what our output would look like and compare it to the input:

>"wouldear intp, enjoy conversation day. esoteric gabbing nature universe idea every rule social code arbitrary construct created... dear entj sub, long time see. sincerely, alpha none them. type hurt deep existential ways want part of. probably slide scale depend individual preferences, like everything humanity. draco malfoy also. would say either  . either  , though stack somewhat arbitrary distinction make believe core indicate primary motivation hand every action. therefore, a... particularly introvert extraverted, personally. said, would say somewhat unphased either social interactions alone. would say crave anything is... dear type  infp, absolute admiration refreshing. great girlfriend wish busy schedule could around one another often. keep...  still mean   people. probably see   others today. never understand fascination virtue rarity. so, esfj train also, right? toy idea op extrovert also awhile now, actually. many conversations him, however disincline believe due op much close fi... still esfj disagree. definite esfj. fe si this. been? mother worry sick. similar feel concern entps. collect shoes. like status nothing communicate thing much pair jordans."

### Tokenizer and padding 
The Tokenizer step converts the sentence into an array of numbers. We define the max_features which is the maximum number of words we want in our vocabulary over the entire document. We then start ranking the words based on how common they are. For example, the most common word would be converted to an integer 1, and the least common word would be converted to an integer 3000 (assuming the maxium features was defined as 3000). We can also define the maximum length of each sample. If we only want to observe 500 words from a post instead of the entire post, we can set the maximum as 500. All the words after 500 words would be discarded and the samples less than 500 words would be "padded" with 0s to make the sample reach 500 words. 

The output is now converted as: 

>array([ 583, 1091,  173,  133,  672,  217, 1832, 2742,  500,  247, 2091,
         99,   13,   16, 2015, 2659,  959,   97,   18,  385,  473,  476,
         15,  148,  165,   82, 1638,  286,  926, 2044,    1,  141, 1678,
         29,    3,   12,  191,  191,   46, 2016,  741,   11,  121, 1191,
       2045, 1521, 1421,  369,  133,  616, 1161,  123,  755,  266, 1280,
        310,  339,    3,   12,  741,  191,  217, 1833,  261,    3,   12,
       2097,   93,   87,  500,   18,   59, 1564,  132,  907,  256, 1065,
       1751,   33,   84,    7,  163,  147,  124,   66,   45,    5,   82,
         16,  119,  283,   42,   73,  143,  336, 1046,   29,   55, 2479,
        173,  700, 1055,   29, 1486,  140,   52,   71,  831,  275,  210,
        121,  550,  700,   20,  213,  204,   66,  336,  839, 2713,  336,
        201,  412,   78, 1271,  433,  462, 1056,  316,   10,  935,  543,
       1861,    1, 1928,  194, 1129,   49,   20, 1391,   57,  120,   75,
          4,  324,   86,  537,   85, 2430, 1296,   53,  383,  969,    4,
         13, 2832,   21,   57,  129, 2814,  217, 1521,  746, 1599,  217,
          1,    5,  523,  664,  145,  308,   38,  259,   61,  357,  419,
         43,  138,  924,   31,    3,  138,   51,   14,  105,   30,  908,
          2,   14,  339,    2,  364, 2621, 2480,  700,   65,  194,  184,
         11,  154,   12,   32,  389,   52,  219,  380,   11,  205, 2602,
        575,  155,    2,  364,   62,   37,  229,    3,   12,   65,  814,
        173,  377,  627,  827,  165,   11,  154,   67,   66, 1446,  641,
        212, 1442,   24,   12,  219,  448,  445,  734,  641,   29, 1844,
        282,  245,  188,   48,  309])


