# Skill Tests
Testing is an important part of skill development. Here are some recommendations
for how to implement good tests for a skill.

## Unit Tests
Like any other module, testing each method in you skill can help prevent debugging
headaches when something goes wrong. These tests are specific to a skill and it
is up to the skill author to test that methods act as expected.

## OSM Installation Tests
This test case may be used to test skill installation via OSM:
```python
import unittest
from os.path import exists
from shutil import rmtree

from ovos_skills_manager import SkillEntry

branch = "dev"  # TODO: Specify default branch
repo = "skill-ovos-volume"  # TODO: Specify repository name
author = "OpenVoiceOS"  # TODO: Specify repository author
url = f"https://github.com/{author}/{repo}@{branch}"


class TestOSM(unittest.TestCase):
    @classmethod
    def setUpClass(self):
        self.skill_id = "{repo.lower()}.{author.lower()}"

    def test_osm_install(self):
        skill = SkillEntry.from_github_url(url)
        tmp_skills = "/tmp/osm_installed_skills"
        skill_folder = f"{tmp_skills}/{skill.uuid}"

        if exists(skill_folder):
            rmtree(skill_folder)

        updated = skill.install(folder=tmp_skills, default_branch=branch)
        self.assertEqual(updated, True)
        self.assertTrue(exists(skill_folder))

        updated = skill.install(folder=tmp_skills, default_branch=branch)
        self.assertEqual(updated, False)
```

## Skill Resource Tests
This test case may be used to test skill resource files and event registration.
A [shared GitHub Action](https://github.com/NeonGeckoCom/.github/blob/master/.github/workflows/skill_test_resources.yml)
is provided by [Neon AI](https://github.com/NeonGeckoCom) to easily implement automated tests. The following files should
be included in the skill repository to use these tests.

### test/test_resources.yaml
This file specifies the expected skill resources, including files, entities, and intent names. An example from the
[Support Helper Skill](https://github.com/NeonGeckoCom/skill-support_helper/blob/dev/test/test_resources.yaml) is
included for reference:

```yaml
# Specify resources to test here.

# Specify languages to be tested
languages:
  - "en-us"

# vocab is lowercase .voc file basenames
vocab: []

# dialog is .dialog file basenames (case-sensitive)
dialog:
  - ask_description
  - cancelled
  - complete
  - confirm_support
  - email_intro
  - email_signature
  - email_title
  - no_email
  - one_moment
  - support
# regex entities, not necessarily filenames
regex: []
intents:
  # Padatious intents are the `.intent` file names
  padatious:
    - contact_support.intent
  # Adapt intents are the name passed to the constructor
  adapt: []
```

### .github/workflows/skill_tests.yml
The filename isn't important here, but a workflow must specify a job using 
`neongeckocom/.github/.github/workflows/skill_test_resources.yml@master`. A minimal example would be:
```yaml
name: Test Skill Resources
on:
  pull_request:
  workflow_dispatch:

jobs:
  skill_resource_tests:
    uses: neongeckocom/.github/.github/workflows/skill_test_resources.yml@master
```

## Skill Intent Tests
This test case may be used to test skill resource files and event registration.
A [shared GitHub Action](https://github.com/NeonGeckoCom/.github/blob/master/.github/workflows/skill_test_intents.yml)
is provided by [Neon AI](https://github.com/NeonGeckoCom) to easily implement automated tests. The following files should
be included in the skill repository to use these tests.

### test/test_intents.yaml
This file specifies skill intents and utterances that should match those intents. Specific vocabulary and entity matches
may also be specified, An example from the
[IP Address Skill](https://github.com/NeonGeckoCom/skill-ip_address/blob/dev/test/test_intents.yaml) is
included for reference:
```yaml
# Specify intents to test here. Valid test cases are as follows:

# Basic intent match tests only:
#lang:
#  intent_name:
#    - example utterance
#    - other example utterance

# Intent tests with expected vocab/entity matches:
#lang:
#  intent_name:
#    - example_utterance:
#        - expected vocab name
#        - other expected vocab name

# Intent tests with specific vocab/entity extraction tests:
#lang:
#  intent_name:
#    - example_utterance:
#        - expected_vocab_key: expected_vocab_value
#        - expected_entity_key: expected_entity_value


en-us:
  IPIntent:
  - what is your ip address
  - what is my ip address:
    - IP
  - what is my i.p. address
  - What is your I.P. address?
  - what is my public IP address?:
    - public: public
```

### .github/workflows/skill_tests.yml
The filename isn't important here, but a workflow must specify a job using 
`neongeckocom/.github/.github/workflows/skill_test_intents.yml@master`. A minimal example would be:
```yaml
name: Test Skill Resources
on:
  pull_request:
  workflow_dispatch:

jobs:
  skill_intent_tests:
    uses: neongeckocom/.github/.github/workflows/skill_test_intents.yml@master
```