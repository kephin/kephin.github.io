# Testing

1. the name of a test file **must** start with `test_`
2. test functions also need to start with `test_`
3. running `pytest` with no argument will run all the tests that `pytest` discovers in the current directory

```python
from name_function import get_formatted_name

def test_first_last_name():
    """Do names like 'Janis Joplin' work?"""
    formatted_name = get_formatted_name('janis', 'joplin')
    assert formatted_name == 'Janis Joplin'
```

| Assertion                  | Claim                                    |
| -------------------------- | ---------------------------------------- |
| assert a == b              | Assert that two values are equal.        |
| assert a != b              | Assert that two values are not equal.    |
| assert a                   | Assert that a evaluates to True.         |
| assert not a               | Assert that a evaluates to False.        |
| assert element in list     | Assert that an element is in a list.     |
| assert element not in list | Assert that an element is not in a list. |

## Testing Class

Consider a AnonymousSurvey class,

```python
class AnonymousSurvey:
    """Collect anonymous answers to a survey question."""

    def __init__(self, question):
        """Store a question, and prepare to store responses."""
        self.question = question
        self.responses = []

    def show_question(self):
        """Show the survey question."""
        print(self.question)

    def store_response(self, new_response):
        """Store a single response to the survey."""
        self.responses.append(new_response)

    def show_results(self):
        """Show all the responses that have been given."""
        print("Survey results:")
        for response in self.responses:
            print(f"- {response}")
```

Write a test_survey function,

```python
from survey import AnonymousSurvey

def test_store_single_response():
    """Test that a single response is stored properly."""
    question = "What language did you first learn to speak?"
    language_survey = AnonymousSurvey(question)
    language_survey.store_response('English')
    assert 'English' in language_survey.responses
```

## Using Fixtures

- When a parameter in a test function matches the name of a function with the `@pytest.fixture` decorator, the fixture will be run automatically and the return value will be passed to the test function 👉 it works just like `beforeEach`.
- A decorator is a directive placed just before a function definition. Python applies this directive to the function before it runs, to alter how the function code behaves.

```python
import pytest
from name_function import get_formatted_name

@pytest.fixture
def languaage_survey():
    """A survey that will be available to all test functions."""
    question = "What language did you first learn to speak?"
    language_survey = AnonymousSurvey(question)
    return language_survey

def test_store_single_response(language_survey):
    # ...
def test_store_three_responses(language_survey):
    # ...
```
