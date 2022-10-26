# Intents

A user can accomplish the same task by expressing their intent in multiple ways. The role of the intent parser is to
extract from the user's speech key data elements that specify their intent in more detail. This data can then be passed
to other services, such as Skills to help the user accomplish their intended task.

_Example_: Julie wants to know about today's weather in her current location, which is Melbourne, Australia.

> "hey mycroft, what's today's weather like?"
>
> "hey mycroft, what's the weather like in Melbourne?"
>
> "hey mycroft, weather"

Even though these are three different expressions, for most of us they probably have roughly the same meaning. In each
case we would assume the user expects Mycroft to respond with today's weather for their current location. The role of an
intent parser is to determine what this intent is.

In the example above, we might extract data elements like:

* **weather** - we know that Julie wants to know about the weather, but she has not been specific about the type of
  weather, such as _wind_, _precipitation_, _snowfall_ or the risk of _fire danger_ from bushfires. Melbourne, Australia
  rarely experiences snowfall, but falls under bushfire risk every summer.
* **location** - Julie has stipulated her location as Melbourne, but she does not state that she means Melbourne,
  Australia. How do we distinguish this from Melbourne, Florida, United States?
* **date** - Julie has been specific about the _timeframe_ she wants weather data for - today. But how do we know what
  today means in Julie's timezone. Melbourne, Australia is between 14-18 hours ahead of the United States. We don't want
  to give Julie yesterday's weather, particularly as Melbourne is renowned for having changeable weather.


OVOS is moving towards a plugin system for intent engines, currently the default MycroftAI intent parsers are still used

Mycroft has two separate Intent parsing engines each with their own strengths. Each of these can be used in most
situations, however they will process the utterance in different ways.

**Padatious** is a light-weight neural network that is trained on whole
phrases. Padatious intents are generally more accurate however require you to include sample phrases that cover the
breadth of ways that a User may ask about something.

**Adapt** is a keyword based parser. It is more flexible, as it detects the
presence of one or more keywords in an utterance, however this can result in false matches.

We will now look at each in more detail, including how to use them in a Mycroft Skill.

## Adapt Intents

Adapt is a keyword based intent parser. It determines user intent based on a list of keywords or entities contained within a users utterance.


### Defining keywords and entities

#### Vocab (.voc) Files

Vocab files define keywords that Adapt will look for in a Users utterance to determine their intent.

These files can be located in either the `vocab/lang-code/` or `locale/lang-code/` directories of a Skill. They can have one or more lines to list synonyms or terms that have the same meaning in the context of this Skill. Mycroft will match _any_ of these keywords with the Intent.

Consider a simple `Potato.voc`. Within this file we might include:

```
potato
potatoes
spud
```

If the User speaks _either_:

> potato

or

> potatoes

or

> spud

Mycroft will match this to any Adapt Intents that are using the `Potato` keyword.

#### Regular Expression (.rx) Files

Regular expressions (or regex) allow us to capture entities based on the structure of an utterance.

We strongly recommend you avoid using regex, it is very hard to make portable across languages, hard to translate and the reported confidence of the intents is not great.

We suggest using padatious instead if you find yourself needing regex

These files can be located in either the `regex/lang-code/` or `locale/lang-code/` directories of a Skill. They can have one or more lines to provide different ways that an entity may be referenced. Mycroft will execute these lines in the order they appear and return the first result as an entity to the Intent Handler.

Let's consider a `type.rx` file to extract the type of potato we are interested in. Within this file we might include:

```
.* about (?P<Type>.*) potatoes
.* (make|like) (?P<Type>.*) potato
```

**What is this regex doing?** `.*` matches zero, one or more of any single character. `(?P<Type>.*)` is known as a Named Capturing Group. The variable name is defined between the , and what is captured is defined after this name. In this case we use `.*` to capture anything.

[Learn more about Regular Expressions](https://github.com/ziishaned/learn-regex/blob/master/README.md).


So our first line would match an utterance such as:

> Tell me about _sweet potatoes_

Whilst the second line will match either:

> Do you like _deep fried potato_

or

> How do I make _mashed potato_

From these three utterances, what will the extracted `Type` be:\
1\. `sweet`\
2\. `deep fried`\
3\. `mashed`

This `Type` will be available to use in your Skill's Intent Handler on the `message` object. We can access this using:

```
message.data.get('Type')
```

### Using Adapt in a Skill

Now that we have a Vocab and Regular Expression defined, let's look at how to use these in a simple Skill.

For the following example we will use the two files we outlined above:

* `Potato.voc`
* `Type.rx`

We will also add some new `.voc` files:

* `Like.voc` - containing a single line "like"
* `You.voc` - containing a single line "you"
* `I.voc` - containing a single line "I"

#### Creating the Intent Handler

To construct an Adapt Intent, we use the intent_handler() \_decorator_ and pass in the Adapt IntentBuilder.

[Learn more about _decorators_ in Python](https://en.wikipedia.org/wiki/Python\_syntax\_and\_semantics#Decorators).

Both of these must be imported before we can use them:

```python
from adapt.intent import IntentBuilder
from mycroft import intent_handler
```

The IntentBuilder is then passed the name of the Intent as a string, followed by one or more parameters that correspond with one of our `.voc` or `.rx` files.

```python
@intent_handler(IntentBuilder('IntentName')
                              .require('Potato')
                              .require('Like')
                              .optionally('Type')
                              .one_of('You', 'I'))
```

In this example:

* the `Potato` and `Like` keywords are required. It must be present for the intent to match.
* the `Type` entity is optional. A stronger match will be made if this is found, but it is not required.
* we require at least one of the `You` or `I` keywords.

What are some utterances that would match this intent?

> Do you like potato? Do you like fried potato? Will I like mashed potato? Do you think I would like potato?

What are some utterances that would _not_ match the intent?

> How do I make mashed potato?

_The required `Like` keyword is not found._

> Is it like a potato?

_Neither the `You` nor `I` keyword is found._

#### Including it in a Skill

Now we can create our Potato Skill:

```python
from adapt.intent import IntentBuilder
from mycroft import intent_handler

class PotatoSkill(MycroftSkill):

    @intent_handler(IntentBuilder('WhatIsPotato').require('What')
                    .require('Potato'))
    def handle_what_is(self, message):
        self.speak_dialog('potato.description')

    @intent_handler(IntentBuilder('DoYouLikePotato').require('Potato')
                    .require('Like').optionally('Type').one_of('You', 'I'))
    def handle_do_you_like(self, message):
        potato_type = message.data.get('Type')
        if potato_type is not None:
            self.speak_dialog('like.potato.type',
                              {'type': potato_type})
        else:
            self.speak_dialog('like.potato.generic')

def create_skill():
    return PotatoSkill()
```

You can [download this entire Potato Skill from Github](https://github.com/krisgesling/dev-ex-adapt-intents-skill/blob/master/\_\_init\_\_.py), or see another Adapt intent handler example in the [Hello World Skill](https://github.com/MycroftAI/skill-hello-world/blob/f3eb89be6d80e1834637a64566c707d05fb8e3fa/\_\_init\_\_.py#L37)


### Common Problems

#### More vocab!

One of the most common mistakes when getting started with Skills is that the vocab file doesn't include all of the keywords or terms that a User might use to trigger the intent. It is important to map out your Skill and test the interactions with others to see how they might ask questions differently.

#### I have added new phrases in the .voc file, but Mycroft isn't recognizing them

1. Compound words like "don't", "won't", "shouldn't" etc. are normalized by Mycroft - so they become "do not", "will not", "should not". You should use the normalized words in your `.voc` files. Similarly, definite articles like the word "the" are removed in the normalization process, so avoid using them in your `.voc` or `.rx` files as well.
2. Tab != 4 Spaces, sometimes your text editor or IDE automatically replaces tabs with spaces or vice versa. This may lead to an indentation error. So make sure there's no extra tabs and that your editor doesn't replace your spaces!
3. Wrong order of files directories is a very common mistake. You have to make a language sub-folder inside the dialog, vocab or locale folders such as `skill-dir/locale/en-us/somefile.dialog`. So make sure that your `.voc` files and `.dialog` files inside a language subfolder.

#### I am unable to match against the utterance string

The utterance string received from the speech-to-text engine is received all lowercase. As such any string matching you are trying to do should also be converted to lowercase. For example:

```python
    @intent_handler(IntentBuilder('Example').require('Example').require('Intent'))
    def handle_example(self, message):
        utterance = message.data.get('utterance')
        if 'Proper Noun'.lower() in utterance:
            self.speak('Found it')
```


## Padatious Intents

Padatious is a [machine-learning](https://en.wikipedia.org/wiki/Machine_learning), [neural-network](https://en.wikipedia.org/wiki/Artificial_neural_network) based _intent parser_. Unlike Adapt, which uses small groups of unique words, Padatious is trained on the sentence as a whole.

Padatious has a number of key benefits over other intent parsing technologies.

* With Padatious, Intents are easy to create
* The machine learning model in Padatious requires a relatively small amount of data
* Machine learning models need to be _trained_. The model used by Padatious is quick and easy to train.
* Intents run independently of each other. This allows quickly installing new skills without retraining all other skill intents.
* With Padatious, you can easily extract entities and then use these in Skills. For example, "Find the nearest gas station" -&gt; `{ "place":"gas station"}`

### Creating Intents

Padatious uses a series of example sentences to train a machine learning model to identify an intent.

The examples are stored in a Skill's `vocab/lang` or `local/lang` directory, in files ending in the file extension `.intent`. For example, if you were to create a _tomato_ Skill to respond to questions about a _tomato_, you would create the file

`vocab/en-us/what.is.a.tomato.intent`

This file would contain examples of questions asking what a _tomato_ is.

```text
what would you say a tomato is
what is a tomato
describe a tomato
what defines a tomato
```

These sample phrases do not require punctuation like a question mark. We can also leave out contractions such as "what's", as this will be automatically expanded to "what is" by Mycroft before the utterance is parsed.

Each file should contain at least 4 examples for good modeling.

The above example allows us to map many phrases to a single intent, however often we need to extract specific data from an utterance. This might be a date, location, category, or some other `entity`.

#### Defining entities

Let's now find out Mycroft's opinion on different types of tomatoes. To do this we will create a new intent file: `vocab/en-us/do.you.like.intent`

with examples of questions about mycroft's opinion about tomatoes:

```text
are you fond of tomatoes
do you like tomatoes
what are your thoughts on tomatoes
are you fond of {type} tomatoes
do you like {type} tomatoes
what are your thoughts on {type} tomatoes
```

Note the `{type}` in the above examples. These are wild-cards where matching content is forwarded to the skill's intent handler.

#### Specific Entities

In the above example, `{type}` will match anything. While this makes the intent flexible, it will also match if we say something like Do you like eating tomatoes?. It would think the type of tomato is `"eating"` which doesn't make much sense. Instead, we can specify what type of things the {type} of tomato should be. We do this by defining the type entity file here:

`vocab/en-us/type.entity`

which might contain something like:

```text
red
reddish
green
greenish
yellow
yellowish
ripe
unripe
pale
```

This must be registered in the Skill before use - most commonly in the `initialize()` method:

```python
from mycroft import MycroftSkill, intent_handler

class TomatoSkill(MycroftSkill):
    def initialize(self):
        self.register_entity_file('type.entity')
```

Now, we can say things like "do you like greenish tomatoes?" and it will tag type as: `"greenish"`. However if we say "do you like eating tomatoes?" - the phrase will not match as `"eating"` is not included in our `type.entity` file.

#### Number matching

Let's say you are writing an Intent to call a phone number. You can make it only match specific formats of numbers by writing out possible arrangements using `#` where a number would go. For example, with the following intent:

```text
Call {number}.
Call the phone number {number}.
```

the number.entity could be written as:

```text
+### (###) ###-####
+## (###) ###-####
+# (###) ###-####
(###) ###-####
###-####
###-###-####
###.###.####
### ### ####
##########
```

#### Entities with unknown tokens

Let's say you wanted to create an intent to match places:

```text
Directions to {place}.
Navigate me to {place}.
Open maps to {place}.
Show me how to get to {place}.
How do I get to {place}?
```

This alone will work, but it will still get a high confidence with a phrase like "How do I get to the boss in my game?". We can try creating a `.entity` file with things like:

```text
New York City
#### Georgia Street
San Francisco
```

The problem is, now anything that is not specifically a mix of New York City, San Francisco, or something on Georgia Street won't match. Instead, we can specify an unknown word with :0. This would would be written as:

```text
:0 :0 City
#### :0 Street
:0 :0
```

Now, while this will still match quite a lot, it will match things like "Directions to Baldwin City" more than "How do I get to the boss in my game?"

_NOTE: Currently, the number of :0 words is not fully taken into consideration so the above might match quite liberally, but this will change in the future._

#### Parentheses Expansion

Sometimes you might find yourself writing a lot of variations of the same thing. For example, to write a skill that orders food, you might write the following intent:

```text
Order some {food}.
Order some {food} from {place}.
Grab some {food}.
Grab some {food} from {place}.
```

Rather than writing out all combinations of possibilities, you can embed them into one or more lines by writing each possible option inside parentheses with \| in between each part. For example, that same intent above could be written as:

```text
(Order | Grab) some {food}
(Order | Grab) some {food} from {place}
```

or even on a single-line:

```text
(Order | Grab) some {food} (from {place} | )
```

Nested parentheses are supported to create even more complex combinations, such as the following:

```text
(Look (at | for) | Find) {object}.
```

Which would expand to:

```text
Look at {object}
Look for {object}
Find {object}
```

There is no performance benefit to using parentheses expansion. When used appropriately, this syntax can be much clearer to read. However more complex structures should be broken down into multiple lines to aid readability and reduce false utterances being included in the model. Overuse can even result in the model training timing out, rendering the Skill unusable.

### Using it in a Skill

The `intent_handler()` _decorator_ can be used to create a Padatious intent handler by passing in the filename of the `.intent` file as a string.

You may also see the `@intent_file_handler` decorator used in Skills. This has been deprecated and you can now replace any instance of this with the simpler `@intent_handler` decorator.

From our first example above, we created a file `vocab/en-us/what.is.a.tomato.intent`. To register an intent using this file we can use:

```python
@intent_handler('what.is.a.tomato.intent')
```

This _decorator_ must be imported before it is used:

```python
from mycroft import intent_handler
```

[Learn more about _decorators_ in Python](https://en.wikipedia.org/wiki/Python_syntax_and_semantics#Decorators).

Now we can create our Tomato Skill:

```python
from mycroft import MycroftSkill, intent_handler

class TomatoSkill(MycroftSkill):

    def initialize(self):
        self.register_entity_file('type.entity')

    @intent_handler('what.is.a.tomato.intent')
    def handle_what_is(self, message):
        self.speak_dialog('tomato.description')

    @intent_handler('do.you.like.intent')
    def handle_do_you_like(self, message):
        tomato_type = message.data.get('type')
        if tomato_type is not None:
            self.speak_dialog('like.tomato.type',
                              {'type': tomato_type})
        else:
            self.speak_dialog('like.tomato.generic')

    def stop(self):
        pass

def create_skill():
    return TomatoSkill()
```

See a Padatious intent handler example in the [Hello World Skill](https://github.com/MycroftAI/skill-hello-world/blob/67a972792a07da7e3406bf7f94acd54aa2674829/__init__.py#L42)

### Common Problems

#### I am unable to match against the utterance string

The utterance string received from the speech-to-text engine is received all lowercase. As such any string matching you are trying to do should also be converted to lowercase. For example:

```python
    @intent_handler('example.intent')
    def handle_example(self, message):
        utterance = message.data.get('utterance')
        if 'Proper Noun'.lower() in utterance:
            self.speak('Found it')
```
