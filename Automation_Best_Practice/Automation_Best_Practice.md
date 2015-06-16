title: Automation Best Practices
theme: jdan/cleaver-retro
author:
    name: ybian
    email: ybian@redhat.com
    irc: ybian
output: Automation_Best_Practice.html

--

### Automation Best Practices

##### Introduction

  * This is not a user guide of [Robot Framework][Robot Framework]

  * This a guide trying to set a Coding Style of our Automation Scripts

  * This is just a draft, and I need your help to build it

[Robot Framework]: http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html

--

### Robot Framework Layers

  * Following picture illustrates the architecture of robot framework automation project

  ![Architecture](/home/ybian/workdir/slides/Automation_Best_Practice/robotframework.png)

  *
    - Test cases file: test suite
    - Resources file: variables and high-level user keywords
    - Library: low-level keywords

--

#### Structure

```
.
├── cases
│   ├── 01__webui
│   │   └── 01__wiki_test.txt
│   └── 02__cmd
│       └── 01__gherkin.txt
├── doc
│   ├── demo_cases_doc.html
│   └── resource_docs
│       ├── cmd_res.html
│       ├── common_res.html
│       ├── home_page.html
│       ├── ride_page.html
│       ├── search_page.html
│       └── wiki_robot_page.html
├── others
│   └── __init__.py
├── resources
│   ├── CalculatorLibrary.py
│   ├── calculator.py
│   ├── cmd_res.txt
│   ├── common_res.txt
│   ├── home_page.txt
│   ├── ride_page.txt
│   ├── search_page.txt
│   └── wiki_robot_page.txt
├── results
│   └── __init__.py
└── scripts
    └── __init__.py

```

--

### Files formats

  * For Test and Resources Format we use  *Plain Text Format*

  * Using *two or more spaces*
    - Do not use *pipe character*

--

#### Tips

  * Tabs or Spaces?
    Spaces
    Or soft-tabs with 2 or 4 space indent, means you need set your editor as "Convert Indentation Spaces"

  * Keep lines fewer than 80 characters, use `...` when it too long

  * Never leave trailing whitespace

  * End of file with a blank newline

--

#### Tips

  * Indent with 4 spaces
    Use at least 4 spaces between columns.

  * Separate tables with two blank lines
    Separate tests or keywords with a single blank line

  * Documatations: best add document for every suite, case, keyword and library

--

#### Naming Conventions

  * Suite Names: use the "lower_case_with_underscores"

  * Test Steps: use the "Given/When/Then"

  * Keyword Names: use the "Cap Words" style

  * Global General Variable Names: use the "${CapWords}"

  * Page Elements Variable Names: use the "${CapWords Locator}"
    NOTE: the "Locator" includes "Locator", "ID", "Name", "Text", "Class", etc.

--

#### Test Suite File:

```
*** Settings ***
Documentation    A test suite with a single test for try page objects
...
...              against the Wikipedia Site
Resource         ../../resources/common_res.txt
Test Teardown    Close All Browsers


*** Test Cases ***
Case 317459 demo show 1
    [Documentation]    This Test Case uses a higher level wikipedia resource
    ...                for showing Page Resource.
    [Tags]             ID_317459    tag1
    Given open browser to wiki home page
    When search for robot framework on wikipedia
    Then from Robot framework wiki page goto RIDE page

Case 317460 demo show 2
    [Documentation]    This Test Case uses a higher level wikipedia resource
    ...                for showing Page Resource.
    [Tags]             ID_317460    tag2
    Then search a string
```

--

#### Resource File:

```
*** Settings ***
Documentation     A resource file containing WiKi home page specific keywords.
...
...               domain specific language. They utilize keywords provided
...               by the imported Selenium2Library.
Library           Selenium2Library
Resource          common_res.txt


*** Variables ***
#************************** Common Variables ******************************
${HomePage URL}              http://${Server}
${HomePage Title}            Wikipedia
${Search Text}               Robot Framework

#************************** Page Elements *********************************
${SearchInput ID}            searchInput
${SearchSubmitButton ID}     go


*** Keywords ***
Open Browser To Wiki Home Page
    [Documentation]       For Open WiKi Home Page.
    Open Browser          ${HomePage URL}             ${Browser}
    Maximize Browser Window
    Set Selenium Speed    ${Delay}
    Title Should Be       ${HomePage Title}

Search For Robot Framework
    [Documentation]       do search operation
    Input Text            ${SearchInput ID}           ${Search Text}
    Click Button          ${SearchSubmitButton ID}

```

--

### Writing Maintainable Automation Scripts

  * Writing Automation is Software Development

--

#### References

  * [Robot Framework Guide](http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html)

  * [PEP8](https://www.python.org/dev/peps/pep-0008/)

  * [Writing Maintainable Automation Scripts](http://dhemery.com/pdf/writing_maintainable_automated_acceptance_tests.pdf)

  * [Anatomy of a good acceptance test](http://gojko.net/2010/06/16/anatomy-of-a-good-acceptance-test/)
