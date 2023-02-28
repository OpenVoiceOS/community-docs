# Voice User Interface Design Guidelines

Through these guidelines you will learn how to use principles of Voice User Interface Design to build more effective
skills. These tools will help define and validate the features of the skill before diving deep into development.

This guide will cover some methods to use that can help plan, prototype and test your skill during the early design stages.

The full original guide can be found over at [the mycroft documentation](https://mycroft-ai.gitbook.io/docs/skill-development/voice-user-interface-design-guidelines)


## Interactions

### Intents

Let's start with an example. A user in Melbourne, Australia might want to know about the weather. To ask for this
information, they might say:

> "Hey Mycroft, what's today's weather like?"
>
> "Hey Mycroft, what's the weather like in Melbourne?"
>
> "Hey Mycroft, weather"

Even though these are three different expressions, for most of us they probably have roughly the same meaning. In each
case we would assume the user expects OVOS to respond with today's weather for their current location.

It is up us as Skill creators to teach OVOS the variety of ways that a user might express the same intent. This is a key
part of the design process. It is the key difference between a Skill that kind of works if you know what to say, and a
Skill that feels intuitive and natural to talk to.

This is handled by an intent parser whose job it is to learn from your Skill what intents it can handle, and extract
from the user's speech and key information that might be useful for your Skill. In this case it might include the
specified date and location.


### Statements and Prompts

You can think of **Prompts** as questions and **Statements** as providing information to the user that does not need a
follow-up response. For example a weather forecast like this would be considered a statement:

> Today’s forecast is sunny with a high of 60 and a low of 45.

#### Statements

For a lot of skills the conversation might end with a simple statement from OVOS, and no further action is necessary.
Try to imagine what the user is trying to accomplish, if a simple statement gets the job done there is no reason to keep
the conversation rolling, and in fact a follow-up might annoy the user with unnecessary interaction.

#### Prompts

It may be tempting to always give users specific instructions like traditional automated phones systems \(Interactive
Voice Response\). Many phone systems are notorious for being too verbose and difficult to follow.

With OVOS we’re trying to break that mold and make the interaction natural. If you follow the phone system method you
may be giving the user the exact phrasing to say, but you’re also taking up valuable time and training them to think the
system is very narrow in capability. In the event that the user does give a response that your skill can not handle,
create follow-up prompts that steer the user back on track.

Remember, there are no errors in a cooperative conversation.

**Avoid**

| Speaker     |                                                                    |
|:------------|:-------------------------------------------------------------------|
| **Mycroft** | _How many people are playing? For example, you can say 2 players._ |

**Better**

| Speaker     |                                              |
|:------------|:---------------------------------------------|
| **Mycroft** | _How many players?_                          |
| **User**    | _My Brother and Myself_                      |
| **Mycroft** | _I’m sorry, what was the number of players?_ |
| **User**    | _Two_                                        |

In the first example the user is told explicitly what they can say, but the prompt is unnatural, we don’t typically
suggest responses to a conversation partner in real life. These long-winded prompts can become tiresome if they are used
repeatedly throughout the skill. Remember the phone system example, typically poorly designed automated phone systems
inundate the user with many options and additional instructions at every step of the interaction.

In the second example we see a better prompt, although the user gives a response that is easy for a human to understand
it is more difficult to design a skill to understand. Instead, the skill designer can apply a re-prompt strategy that
steers the user back on track and doesn't require them to start the interaction over. In this case the re-prompt changes
the wording slightly to make it clear that the user needs to say a number. The next time the user interacts with this
Skill, they will likely say a number in their first interaction.

Determining whether to respond to the user with a statement or a prompt can be a bit tricky. When the user is
somewhat vague it is tempting to assume the user’s intent in order to speed along the interaction. Sometimes this is the
right approach and sometimes it is not. If you are very confident in the user’s input then it is alright to assume, and
respond with a statement. For example in the Wikipedia Skill the Wikipedia API is used to confidently select the best response.

**Wikipedia Skill**

| Speaker     |                                                                                                                                                                                                                                                   |
|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **User**    | _Tell me about Abraham Lincoln_                                                                                                                                                                                                                   |
| **Mycroft** | _Abraham Lincoln was an American statesman and lawyer who served as the 16th president of the UnitedStates from 1861 to 1865. Lincoln led the nation through its greatest moral, constitutional, and political crisis in the American Civil War_. |

In contrast, let’s look at an example of where a follow-up prompt is a better approach. You’re working on a skill that
gives important information about birds, such as wingspan, laden and unladen airspeed, etc..

**Avoid**

| Speaker     | \*\*\*\*                                                               |
|:------------|:-----------------------------------------------------------------------|
| **User**    | _what is the airspeed velocity of an unladen swallow?_                 |
| **Mycroft** | _The unladen airspeed of the european swallow is 20.1 miles per hour._ |

**Better**

| Speaker     |                                                                        |
|:------------|:-----------------------------------------------------------------------|
| **User**    | _What is the airspeed velocity of an unladen Swallow?_                 |
| **Mycroft** | _What do you mean, African or European Swallow?_                       |
| **User**    | European Swallow.                                                      |
| **Mycroft** | _The unladen airspeed of the European Swallow is 20.1 miles per hour._ |

In the first example Mycroft assumes the user is referring to the European Swallow, however there is nothing to give
confidence to that assumption. In this case it’s dangerous to assume the User meant the European Swallow since it is
just as likely they meant the African Swallow. When there is no confidence in one answer versus another, OVOS should
follow up with a prompt as demonstrated in the second example.

Another approach to solving this problem is to offer the most likely answer and inform the user that there are other
answers available with a statement.

### Confirmations

Confirmation approaches can also be defined by Statements or Prompts , but when we talk about them in the context of
confirmations we call them Implicit and Explicit.

#### Implicit Confirmation

This type of confirmation is also a statement. The idea is to parrot the information back to the user to confirm that it
was correct, but not require additional input from the user. The implicit confirmation can be used in a majority of
situations. For example Mycroft’s Timer Skill uses implicit confirmation when creating new timers.

**Timer Skill**

| Speaker     |                                          |
|:------------|:-----------------------------------------|
| **User**    | _Hey Mycroft set a timer for 5 minutes_  |
| **Mycroft** | _Alright, I’m starting a 5 minute timer_ |

**Avoid**

| Speaker     |                                                |
|:------------|:-----------------------------------------------|
| **User**    | _Hey Mycroft, add bananas to my shopping list_ |
| **Mycroft** | _done_                                         |

**Better**

| Speaker     |                                                |
|:------------|:-----------------------------------------------|
| **User**    | _Hey Mycroft, add bananas to my shopping list_ |
| **Mycroft** | _Adding bananas_                               |

#### Explicit Confirmation

This type of confirmation requires an input from the user to verify everything is correct. Only use explicit
confirmation when needed as it can be tedious for the user to always confirm their input. This strategy is best when
there are multiple steps, and it would be difficult to fix a misstep without starting over, or when deleting or
modifying an existing multistep input.

**Avoid**

| **Speaker** |                                                                |
|:------------|:---------------------------------------------------------------|
| **User**    | _Hey Mycroft, set an alarm for 9:00 am tomorrow_               |
| **Mycroft** | _Ok, I’ve set an alarm for 9:00 am tomorrow, is that correct?_ |
| **User**    | _Yes_                                                          |
| **Mycroft** | _9:00 am alarm set_                                            |

**Better**

| Speaker     |                                                              |        
|:------------|:-------------------------------------------------------------|
| **User**    | _Hey Mycroft, set an alarm for 9:00 am tomorrow_             |        
| **Mycroft** | I've set an alarm for tomorrow at 9:00 am, 16 hours from now |        

The first example requires the user to confirm the alarm. Since the interaction is quite short it isn’t necessary to use
explicit confirmation.

**Avoid**

| **Speaker** |                                                                               |
|:------------|:------------------------------------------------------------------------------|
| **User**    | _Hey Mycroft, set a calendar event for a meeting with Chris Stevens_          |
| **Mycroft** | _When is the event?_                                                          |
| **User**    | _Tomorrow at 11:00 am_                                                        |
| **Mycroft** | _should I send an invite to Chris Stevens?_                                   |
| **User**    | _Yes_                                                                         |
| **Mycroft** | _Alright, I've created a meeting for Tomorrow_                                |
| **Mycroft** | _Alright, I’ve created a meeting for Tomorrow at 11:00 am with Chris Stevens_ |
| **User**    | _Cancel my 11:00 am meeting tomorrow_                                         |
| **Mycroft** | _Done_                                                                        |

**Better**

| Speaker     |                                                                               |
|:------------|:------------------------------------------------------------------------------|
| **User**    | _Hey Mycroft, set a calendar event for a meeting with Chris Stevens_          |
| **Mycroft** | _When is the event?_                                                          |
| **User**    | _Tomorrow at 11:00 am_                                                        |
| **Mycroft** | _should I send an invite to Chris Stevens?_                                   |
| **User**    | Yes                                                                           |
| **Mycroft** | _Alright, I’ve created a meeting for Tomorrow at 11:00 am with Chris Stevens_ |
| **User**    | _Cancel my 11:00 am meeting tomorrow_                                         |
| **Mycroft** | _Are you sure you want to delete your meeting tomorrow at 11:00 am?_          |
| **User**    | _Yes_                                                                         |

Both examples use explicit and implicit confirmation correctly until the end of the interaction when the user wants to
cancel the event. Unlike setting a simple timer or an alarm creating this calendar event requires multiple steps and
would require reasonable effort to recreate. There may also be significant consequences if the request was
misinterpreted and the meeting was cancelled unintentionally.

## Conversations

Any time the user needs to input a lot of information or the user needs to sort through a variety of options a conversation will be needed.
Users may be used to systems that require them to separate input into different chunks. 
For example, many personal navigation devices \(GPS units\) require users to input the street number, street name, city, and state separately, like this:

| Speaker               |                             |
|:----------------------|:----------------------------|
| **Navigation Device** | _What is the street number_ |
| **User**              | _123_                       |
| **Navigation Device** | _What is the street name_   |
| **User**              | _Main Street_               |
| **Navigation Device** | _What is the city_          |
| **User**              | _Springfield_               |
| **Navigation Device** | _Oregon_                    |

This was a limitation of the technology, both the STT and intent parser were not capable of handling an entire address. 
With OVOS you do not need to separate the address into multiple inputs. 
It’s also easy to think like a traditional GUI and translate what are typically separate fields into prompts for the user,
but that will only slow down the interaction. 

The best solution is to allow the user to input information both ways, all at once, or in pieces. 
For example the Alarm skill allows the user to set a complicated alarm all in one go, or in steps.

**In Steps:**

| Speaker     |                                                 |
|:------------|:------------------------------------------------|
| **User**    | _Hey Mycroft, set a recurring alarm_            |
| **Mycroft** | _For what day?_                                 |
| **User**    | _weekdays_                                      |
| **Mycroft** | _For what time?_                                |
| **User**    | _7 am_                                          |
| **Mycroft** | I've set a recurring Alarm for 7 am on weekdays |

**All at once:**

| Speaker  |                                                         |
|:---------|:--------------------------------------------------------|
| **User** | Hey Mycroft, set a recurring alarm for weekdays at 7 am |
| Mycroft  | I've set a recurring Alarm for 7 am on weekdays         |

### Context

Conversational context is a given when speaking to another person, but not always when interacting with a computer based system. Many skills are designed with only a quick back and forth interaction in mind, and can operate well without conversational context, but conversational context can be a powerful addition to a skill and can make the interaction much more life like. Here are some examples of how to use context in conversation. 

| Speaker     |                                                                                                                                                                                                                                          |
|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **User**    | _Who is Shaquille O'Neal_                                                                                                                                                                                                                |
| **Mycroft** | _Shaquille O'Neal is an American former professional basketball player who is a sports analyst on the television program Inside the NBA on TNT. He is considered one of the greatest players in National Basketball Association history_ |
| **User**    | _How tall is he?_                                                                                                                                                                                                                        |
| **Mycroft** | _seven foot 1 inches tall_                                                                                                                                                                                                               |
| **User**    | _when did he retire_                                                                                                                                                                                                                     |
| **Mycroft** | _2011_                                                                                                                                                                                                                                   |


## Error Handling

Inevitably, the user will say something that your skill can’t handle. It’s best not to think of these as errors on the part of the user, remember there aren’t really errors in conversations. Conversations are naturally cooperative with both parties seeking to continue to a successful outcome. Keeping that in mind you should do your best to avoid Error Handling that is a dead-end.

**Avoid**

| Speaker     |                                        |
|:------------|:---------------------------------------|
| **User**    | _Timer_                                |
| **Mycroft** | _I'm sorry I can't help you with that_ |

**Better**

| **Speaker** |                         |
|:------------|:------------------------|
| **Use**r    | _Timer_                 |
| **Mycroft** | _A timer for how long?_ |
| **User**    | _5 minutes_             |

In the first example OVOS does not give the user any options to finish the job they set out to do. Try to avoid situations where the user has to start the conversation over.
