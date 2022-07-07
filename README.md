# Automatzen Hackathon 2022

This is a documention library for custom created keywords in the Learning Pool Automation Suite.

## Installation

Please see the following to set up the automation framework: [Set Up Guide](https://learninglocker.atlassian.net/wiki/spaces/QS/pages/3555885080/Install+and+Set+up+for+Robot+Framework+QA+WINDOWS+SET-UP)

## Using Keywords

A keyword is a single test step. Just as a test is conceptually made up of many steps, a robot test is made up of many keywords. Keywords are the foundation upon which all robot tests are built.

We have created our own keywords so that tests can focus on the test logic rather than the underlying implementation.

For example, let's consider what an acceptance test for logging in might be. From the perspective of an agile product owner or lead designer, it might look something like this:

```python
Open a browser to the url
Enter a valid username
Enter a valid password
Click the Login button
You should be on the dashboard page
```
This might be literally what the product owner adds as acceptance criteria on a story card or in a ticket tracking system. Wouldn't it be nice if that was an actual test which someone could run?

## Example Test Case

Each one of those steps could be considered a keyword. One of the great things about robot is that you can write a test that looks almost identical to the original specification:

```python
*** Test Cases ***
TC_01_As An Orgadmin Login To Stream
    [Documentation]    Verifies OrgAdmin user can login to Stream
    Login To Stream    ${ORG_ADMIN_USERNAME}    ${GLOBAL_PASSWORD}
    Assert User Dashboard Has Loaded
```

## Keyword Implementation Example

To make this test case run, you will need to define these keywords since robot doesn't know what "Login To Stream" means. We use the browser library built in keywords to create this:

```python
*** Keywords ***
Login To Stream
    [Documentation]    Inputs the user login details and logs user on application
    [Arguments]    ${user_name}    ${user_password}
    Fill Text    ${USERNAME_TEXTBOX}    ${user_name}
    Fill Secret    ${PASSWORD_TEXTBOX}    $user_password
    Click    ${LOGIN_BUTTON}
    Wait Until Network Is Idle    timeout=${LARGE_WAIT}
```
