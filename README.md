# Lectures on Machine Learning Methods for Cosmology

[ICTP-SAIFR School on Cosmology](https://www.ictp-saifr.org/ictptriestesc2025/)

**Day 1**. [Slides](https://docs.google.com/presentation/d/1IV9PqR0Rofjxz3kRqQlTco-iCodBbT6iBHQIExwX-ec/edit?usp=sharing). [Notebook1](https://colab.research.google.com/github/franciscovillaescusa/ML_lectures/blob/main/Pytorch.ipynb). [Notebook2](https://colab.research.google.com/drive/1e846wc10-bQgxqPUJMlo-VBA2aHW77d5?usp=sharing). [Data](https://github.com/franciscovillaescusa/ICTP-SAIFR/tree/main/Day1/data)

**Day 2**. [Slides](https://docs.google.com/presentation/d/1EP7U3QJrYvaQopYFjOYybEQ6s95FiFQeh5SWq6vs6Jc/edit?usp=sharing). [Notebook](https://colab.research.google.com/github/franciscovillaescusa/ML_lectures/blob/main/Lecture2.ipynb). [Data](https://www.dropbox.com/sh/vghnick9hr1gksr/AADPV4FMPsWpurnSl9kXZjp1a?dl=0)

**Day 3**.  [Slides, notes, and supplemental material](https://udlbook.github.io/udlbook/)

**Day 4**. [Slides](https://docs.google.com/presentation/d/10GcXycXYh2H6W0_ZJeqeNm5U14tStrxoqPUFZGRDn-c/edit?usp=sharing). [Notebook](https://colab.research.google.com/drive/10aIz1dgQIy6fjYtq4-r4vbvEMclRs7xi?usp=sharing). 

**Day 5**. [Slides](https://docs.google.com/presentation/d/1g08FbE1jaElYDip3IHoZ3Zq0HPtl4OiI1VToMMX1oIo/edit?usp=sharing). [Generated papers](https://github.com/franciscovillaescusa/ICTP-SAIFR/tree/main/Generated_papers)

## Day 4 
- Get a [gmail](https://mail.google.com/) account if you dont have one 
- Get a Gemini API key. Go [here](https://ai.google.dev/gemini-api/docs/api-key) and click on the link in the first line. Do not share this key with anyone or upload it to GitHub or any other public website.


## Day 5
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
#astro_pilot.get_results()
#astro_pilot.get_results(engineer_model='gemini-2.5-pro', researcher_model='gemini-2.5-pro')

# Write a paper with [APS (Physical Review Journals)](https://journals.aps.org/) style
#astro_pilot.get_paper(journal=Journal.AAS, llm='gemini-2.5-flash', add_citations=True)
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

## Generated papers evaluation

- X-ray paper assestment from Isabel Pederneiras:

``
The paper used data from the recently published CODEX cluster catalog (Pederneiras et al. 2025) to compare the mass–X-ray luminosity relations of galaxy clusters observed by ROSAT (DR3, Voges et al. 1999) and eROSITA (DR1, Merloni et al. 2024), focusing on the systematic differences between the two surveys. The idea was relevant, and the abstract, introduction, and plots were carefully prepared. Nonetheless, the execution suffered from a mistake in unit conversion that produced non-physical luminosity values. In addition, the fitting method, although technically correct, was overly simplistic and had already been employed in earlier studies (e.g. Chen et al. 2007; Eckmiller et al. 2011). The text also suffered from unnecessary repetitions, an excessive subdivision into sections, and awkward figure references, which reduced its clarity. Overall, while the motivation and some aspects of the presentation were strong, the methodological issues and lack of originality in the analysis would prevent the work from reaching current journal standards.
``

## Resources
- [Understanding deep learning book](https://udlbook.github.io/udlbook/)

## Contact

fvillaescusa@flatironinstitute.org
