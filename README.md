<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=Abinivesh %20Mayilsamy&fontSize=80&animation=fadeIn" alt="Header" />
</div>

<h1 align="center">Hi there, I'm <a href="https://github.com/AbiniveshMayilsamy" target="_blank">Abinivesh Mayilsamy</a>! 👋</h1>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=F7F7F7&background=00000000&center=true&vCenter=true&width=435&lines=Full+Stack+Developer;Open+Source+Enthusiast;Always+Learning" alt="Typing SVG" />
</p>

---

### 🧐 About Me

- 🌱 I’m currently learning **React, Python, and AWS**
- 👯 I’m looking to collaborate on **Open Source Projects**
- 💬 Ask me about **Web Development, Tech, and Design**
- 📫 How to reach me: **abiniveshmayilsamy@gmail.com**

---

### 🛠️ Languages and Tools
<p align="left">
  <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="40" height="40"/> </a> 
  <a href="https://reactjs.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original.svg" alt="react" width="40" height="40"/> </a> 
  <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a>
  </p>

---
name: Generate Snake

on:
  # Run automatically every 12 hours
  schedule:
    - cron: "0 */12 * * *" 
  
  # Allows to manually run the job at any time
  workflow_dispatch:
  
  # Run on every push on the master branch
  push:
    branches:
    - master
    - main

jobs:
  generate:
    permissions: 
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5
    
    steps:
      # Generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          
      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
