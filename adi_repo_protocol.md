[200~Here is the detailed `README.md` for your **LightRAG Fork**. You can copy and paste this directly into a `README-THESIS.md` file (or replace the original `README.md` at the 
root of your fork) so you always have a cheat sheet for your Git workflow. *** ```markdown
# LightRAG (Text2Cypher Thesis Fork)
This repository is a customized fork of the original [LightRAG](https://github.com/HKUDS/LightRAG) framework. It has been modified to support Text2Cypher tasks and graph 
database integrations as part of my Master's thesis research.
> **⚠️ CRITICAL RULE FOR THIS REPO ⚠️** **NEVER make commits directly to the `main` branch.** > The `main` branch is strictly reserved as a mirror of the original LightRAG 
> upstream repository. All thesis development must happen on the `text2cypher` branch.
---
## 📂 1. How This Fits Into the Thesis
This repository acts as the **engine**. It is designed to run side-by-side with the main thesis repository (which contains the experiments, Jupyter Notebooks, and evaluations). 
**Directory Setup on Local Machine:** ```text workspace/
 ├── LightRAG-fork/ <-- (This repository) Core engine & Text2Cypher modifications └── my-thesis/ <-- Notebooks, data, evaluation scripts, and PDF ``` **To use this engine in the 
thesis repository:** Navigate to the `my-thesis` folder, activate the virtual environment, and run an editable install: ```bash cd ../my-thesis source venv/bin/activate pip 
install -e ../LightRAG-fork ``` *Note: Because of the `-e` flag, any code changes saved in this fork are instantly available in the thesis notebooks. No re-installation is 
required.* ---
## 🛠️ 2. Daily Development Workflow
Whenever you sit down to write code for the Text2Cypher implementation, ensure you are on the correct branch. **1. Check your current branch:** ```bash git status ``` *Ensure it 
says `On branch text2cypher`.* **2. If you are not on the branch, switch to it:** ```bash git checkout text2cypher ``` **3. Standard coding loop:** Write your code, test it, and 
commit your changes regularly to save your progress: ```bash git add . git commit -m "feat: added new cypher prompt template" git push origin text2cypher ``` ---
## 🔄 3. Upstream Sync Guide (The "Airlock" Method)
The original LightRAG repository updates continuously. Follow these exact steps to pull their newest features into your thesis work safely, without overwriting your Text2Cypher 
modifications.
### Step A: Verify Upstream is Connected (One-time setup)
Check if the original repository is linked to your local clone: ```bash git remote -v ``` If you do not see `upstream` pointing to the original LightRAG repo, add it: ```bash 
git remote add upstream [https://github.com/HKUDS/LightRAG.git](https://github.com/HKUDS/LightRAG.git) ```
### Step B: Syncing the Code (Perform every few weeks)
**1. Secure your current work:** Make sure all your `text2cypher` changes are committed. You should have a clean working tree. ```bash git status ``` **2. Switch to the delivery 
bay (`main`):** ```bash git checkout main ``` **3. Download the newest LightRAG updates:** ```bash git fetch upstream ``` **4. Update your local `main` branch:** ```bash git 
merge upstream/main ``` **5. Update your GitHub fork's `main` branch:** ```bash git push origin main ``` *(Your `main` branch is now perfectly identical to the latest official 
LightRAG version).* **6. Bring the updates to your workbench:** Switch back to your thesis branch: ```bash git checkout text2cypher ``` **7. Merge the new updates into your 
custom code:** ```bash git merge main ```
### 🚨 Step C: Handling Merge Conflicts
If Step B7 results in a `Merge Conflict`, it means LightRAG updated the exact same lines of code you modified for Text2Cypher. * Do not panic. * Open your code editor (e.g., VS 
Code). It will highlight the conflicting files. * Choose to "Accept Current Change" (your code), "Accept Incoming Change" (their code), or manually combine both. * Once 
resolved, save the files and run:
  ```bash git add . git commit -m "chore: resolved merge conflicts with upstream main" ``` * **Emergency Abort:** If the conflict is too messy and you want to undo the update, 
simply run `git merge --abort`. This safely returns your `text2cypher` branch to how it was before Step B7.
```
