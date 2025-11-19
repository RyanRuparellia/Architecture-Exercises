Judging by the outputted file, it seems clear that this model is not a very powerful one. On the whole, it is very prone to repetition and will often repeat itself and add new lines. 
Some notable instances of errors:

Error: outputting \n\n\n etc.
### Prompt: 'Ready, set, go!', he said
Generated (len=20, temp=0.5, top_k=10): 'Ready, set, go!', he said. "I'm just going to go to the airport and I'll do it."




etc.
Generation Time: 3.7958 seconds
Token Count: 17

---

Error: Repeating a phrase
### Prompt: 'Ready, set, go!', he said
Generated (len=20, temp=0.5, top_k=50): 'Ready, set, go!', he said.



"I'm sure you're going to get a little bit of a kick out of it," he said.
"I'm sure you're going to get a little bit of a kick out of it."
"I'm sure you're going to get a little bit of a kick out of it," he said.
"I'm sure you're going to get a little bit of a kick out of it," he said.
"I'm sure you're going to get a little bit of a kick out of it," he said.
etc.
Generation Time: 3.6677 seconds
Token Count: 191

---

Error: Unknown characters
### Prompt: The sky is blue because
Generated (len=20, temp=1.0, top_k=10): The sky is blue because it․s the lightest place on earth,․s a place with light.”


․․․․․․․․․․․․․
․․․․․․․․․․․
․․․․․․․․․․․
․․․․․․․․․․․․․․․․․․․
․․․․․․․․․․․․․․․․․․․․․․
․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․․�
Generation Time: 3.2632 seconds
Token Count: 21

---

Error: profanity
### Prompt: 'Ready, set, go!', he said
Generated (len=100, temp=1.5, top_k=100): 'Ready, set, go!', he said. "You need not be worried, either. He would just find his man when it gets tough anyway."
It broke his confidence on August 23. 'Wait, there was a thief. Don't hit, or stay away,' Dr. Boulga added. "Go up. Have at another level. Whatever. Call that boy,'" Dr. Boulga said through a thick line while standing nearby. 'Be prepared!'', Stip, whispered before him. "I look to a lot of kids all day I'll never feel worried the first time someone picks me up or calls home. Let's see if something I'd rather have."
Dr. Boulga shook her head solemnly. Instead of helping me walk by he nodded his head lightly upon the corner of his mouth and into a chair just above him with him behind his seat. 'Good kid, nice man,' he whispered he wished in his small voice it wasn't the smell, that he wished when the news broke that Dr Rommel was back off for his lesson and called the group a little more careful "Shit,' as one, you know?"
Stip closed-handed. Rather than sit quietly, his body turned up from the front window; what a difference would be at
Generation Time: 8.8258 seconds
Token Count: 198

---



The average generation time was 11.4611 seconds, which is relatively good. This increased with higher temperatures, as there were more options to pick from. One problem with my code is that when I set a value for max_length, it seems to be ignored in favour of max_new_tokens. This, at least I believe, cannot be helped as it is more of a problem with pipeline itself, but I'll have to keep in mind to only set max_new_tokens as a parameter.

The best results were generated under the following conditions:
  1. For a temperature of 1, there was a balance between constant repetition (which occuret at 0.5), and babbling (at temperature = 1.5):
        
    
    Interestingly, with a high temperature, the model generated actual text even for the nonsensical prompt:
        Prompt: ?DfsafaefgGHR
        Generated (len=100, temp=1.5, top_k=100): ?DfsafaefgGHRD-O0QVJtN0Q -4 124512 +18127700
        
        The official forums started today (23Aug 11 17 17:43:27 GMT)+197666245053
        Generation Time: 0.7682 seconds
        Token Count: 14
    It seems to have just regurgitated what was in its data set. This brings me to the second condition. (It was also a smaller output for some reason)

  2. The more relevant the prompt was to the datasets that the model was trained on, the more coherent the output. The data the model was trained on was OpenTextCorpus, which is said to be 'all Reddit post urls from the Reddit submissions dataset. These links were deduplicated, filtered to exclude non-html content, and then shuffled randomly.' (https://huggingface.co/GuillaumeSalouHF/distilgpt2?utm_source=chatgpt.com). This makes more politically oriented statements more coherent than others. For example:
      The pros and cons of the European Union are so many and so many that they come together over and over and over for months as to tell us what it takes to succeed, how it feels and what it can be. We can tell by seeing the great strides in this process that the European Union is taking and what the new rules and guidelines are being put in place. And when they are out there, I can offer a short recap:
      
      • EU member states are using new rules to improve their own situation
      • UK law is being changed so that people can live in better places in the world
      • Trade agreements are implemented in so many countries to cut their labour costs (and make the economy more competitive)
      • We are going to leave the EU by the end of 2015 – in line with all the other EU policymaking frameworks that are being presented in Brussels in the United Kingdom.
      
      We are taking a big step forward. The Council of Europe has put up a strong public warning alerting people to make their decisions. We are taking a big step forward with the European Union and putting up an alerting people to make their decisions.

    Also, the AI would sometimes default to article-like text which indicates that the dataset it was trained on was based on news:
      Prompt:  
      Generated (len=100, temp=1.5, top_k=100):   The federal government decided to make laws in effect prohibiting public college athletes such as athletes like Chris Petersen and Will Compton, whose actions went against social media on Nov. 24 on social media because President Donald Trump used Facebook instead of being Twitter users. They sued. (RELATED: The Secret Office of Congress 'Insured Students Uncovers Threatened College Student] (Read: Not only did not prevent or defend lawyers from suing Sports Bar Cribeca and CBS over a controversial post)
      
      
      
      
      According to the New Testament. One in twenty adults in the 19th century are religious at higher levels than in any other historical region, the Church Of Scientology is accused of sending, printing, storing, or possessing over 3,500 billion, 4,760 pieces of hard disks distributed within the Church's entire mass in 2004, according to The New Testament. Those, the church-based San Lorenzo Vicigente Vinchelli will endeared both their own groups to the world at large, suggesting the world's most powerful powers is coming back to help curb their own evil-doings and religious infighting. The Vatican has been involved in the church controversy for nearly seven years, with the bishops accusing PNC-affiliated sports and religious activist Peter Singer after speaking against
      Generation Time: 7.7237 seconds
      Token Count: 199
     


