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
case we would assume the user expects OVOS to respond with today's weather for their current location. The role of an
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


OVOS has two separate Intent parsing engines each with their own strengths. 
Each of these can be used in most situations, however they will process the utterance in different ways.

**Example based** intents are trained on whole phrases. These intents are generally more accurate however require you to include sample phrases that cover the
breadth of ways that a User may ask about something.

**Keyword / Rule based ** these intents look for specific required keywords. They are more flexible, but since these are essentially rule based this can result in a lot of false matches.
A badly designed intent may totally throw the intent parser off guard. The main advantage of keyword based intents is the integration with [conversational context](../context), they facilitate continuous dialogs

OVOS is moving towards a plugin system for intent engines, currently only the default MycroftAI intent parsers are supported

- **Padatious** is a light-weight neural network that is trained on whole phrases. You can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/mycroft-technologies/padatious)
- **Adapt** is a keyword based parser. You can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/mycroft-technologies/adapt)

