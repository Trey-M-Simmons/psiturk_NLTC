# NaturalLanguageToRobotCommands
This is a portion of an experiment where participants will be asked to aid a simulated robot (specifically an Astrobee) place cargo into different locations. This code specifically uses an LLM to convert natural human language into commands that the robot can understand.

# Environment
For context, we are using Purdue Lafayettes hosted LLMs that are free for students and facualty(I do not believe that they are available otherwise), 
there is not currently support for other LLMs. If you are a Purdue student then you can get an API key using: https://genai.rcac.purdue.edu/
Once you have signed in using your Purdue Credentials and are on the main chat page, click on your name in the bottom left corner. Then click "account" under 
the profile section. Then under the API key section at the bottom of the window create a new API key.

Otherwise:
Ubtuntu 24.04 
python 3.8
Please take a look at NLTC_requirements.txt to see all of the libraries


# RUN
1. Source .NLTC_Venv or create your own venv
    source .NLTC_Venv/bin/activate
    or 
    (assumes that you have uv and python 3.8 installed in uv)
    uv venv --python 3.8 .venv 
    uv pip install -r NLTC_requirements.txt
    source .venv/bin/activate

2. export API key
    export GENAI_API_KEY="Your API key"

3. Run tests using pytest
    cd to the "Testing" folder
    pytest -v
    or 
    run pytest with whatever flags that you like


# Future Fixes
Currently the model + program consistently succeed except for the valid prompts asking for the cargo to be placed on the left/right/middle ones

# Important Notes
Note: As of Oct 28, 2026, this code will actually be a integrated into Psiturk and be an independant repository.