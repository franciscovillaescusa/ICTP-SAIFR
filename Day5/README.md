In order to use Denario (a multi-agent system designed to carry out end-to-end scientific research) follow these steps:

- Get a [gmail](https://mail.google.com/) account if you dont have one 
- Get a Gemini API key. Go [here](https://ai.google.dev/gemini-api/docs/api-key) and click on the link in the first line. Do not share this key with anyone or upload it to GitHub or any other public website.
- Check that your key work. E.g. try it with the [CAMELS Agents](https://camels-agents.streamlit.app/). Select Gemini-2-flash and write CAMELS section and click select task. If some text is printed your key is active.
- Install [Denario](https://github.com/AstroPilot-AI/Denario):
  - git clone https://github.com/AstroPilot-AI/Denario.git
  - cd Denario
  - python3 -m venv Denario_env
  - source Denario_env/bin/activate
  - pip install -e .

- Set the keys
  - create a file called .env
  - Inside .env set:
  ```sh
  # Gemini API key
  GOOGLE_API_KEY=Your_gemini_key_here
  GOOGLE_APPLICATION=gemini.json

  # OpenAI API key
  OPENAI_API_KEY=Your_openay_key_here
  ```
 
- To check that it works, create a file called run.py and put:
```python
from denario import Denario, Journal

folder = "Project1"

# set AstroPilot and input text
astro_pilot = Denario(project_dir=folder)
astro_pilot.set_data_description(f"{folder}/input.md")

# Generate a research idea from the input text
astro_pilot.get_idea_fast(llm='gemini-2.5-flash')

# Generate a research plan to carry out the idea
astro_pilot.get_method_fast(llm="gemini-2.5-pro")

# Follow the research plan, write and execute code, make plots, and summarize the results
#astro_pilot.get_results() #comment out this line to use GPT + Claude Sonnet
#astro_pilot.get_results(engineer_model='gemini-2.5-pro', researcher_model='gemini-2.5-pro') #comment out this line to use gemini-2.5-pro

# Write a paper with [APS (Physical Review Journals)](https://journals.aps.org/) style
#astro_pilot.get_paper(journal=Journal.AAS, llm='gemini-2.5-flash', add_citations=True) #comment out this line to write a paper
```

- Create a folder called Project1
- Inside Project1, put a file called input.md
- Inside input.md put your prompt

If you want to run the get_results module with GPT alone, do this:
```python
astro_pilot.get_results(engineer_model='o3-mini', researcher_model='o3-mini')
```

If you want to run the get_results module with Gemini, you need a file called gemini.json. To get it, follow these instructions:
- Log into Google Cloud: https://console.cloud.google.com/
- Create a project
- Go to IAM & Admin
- Go to Service Accounts
- Create a Service Account
- Choose a name
- Create and Continue
- Grant the "Vertex AI User" role
- Click Continue and then Done
- Click on the three dots and Manage keys
- Add key --> Create new key --> JSON --> Create
- Change the name of that file to gemini.json

You may already have plots and results and want to write a paper with it. To achieve that, you should:
- Create a project folder, e.g. Project2
- Inside Project2, create a folder called plots. Put all your plots inside this folder.
- Inside Project2, create a file called idea.md that should contain a short description of the idea behind the paper and the title of the paper, if you have one
- Inside Project2, create a file called methods.md that should contain a description of the methods used and potentially the outline of the paper
- Inside Project2, create a file called results.md that should contain a description of the results obtained

After this, you can write the paper with this:

```python
from denario import Denario, Journal

folder = "Project2"

# set AstroPilot and input text
astro_pilot = Denario(project_dir=folder)

# Write a paper with [APS (Physical Review Journals)](https://journals.aps.org/) style
astro_pilot.get_paper(journal=Journal.AAS, llm='gemini-2.5-flash', add_citations=False)
```