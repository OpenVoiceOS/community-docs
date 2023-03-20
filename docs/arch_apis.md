# APIs

## Skill API

The Skill API uses the Message Bus to communicate between Skills and wraps the interaction in simple Python objects making them easy to use.

### Limitations

The Skill API works over the Message Bus. This requires that the return values are json serializable. All common Python builtin types \(such as List, String, None, etc.\) work well, however custom classes are not currently supported.

## Using another Skill's API

If you want to make use of exported functionality from another Skill, you must fetch that Skill's `SkillApi`. This will give you a small class with the target Skill's exported methods. These methods are nothing special and can be called like any other class's methods.