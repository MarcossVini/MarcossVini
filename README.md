from pathlib import Path
import zipfile, textwrap

base = Path("/mnt/data/marcos-github-profile")
workflow_dir = base / ".github" / "workflows"
workflow_dir.mkdir(parents=True, exist_ok=True)

readme = r'''<div align="center">

# Marcos Vinicius

**Software Engineer · Backend & FullStack Developer**

Building software with a focus on **backend engineering, system design and reliable applications**.

[LinkedIn](https://linkedin.com/in/engmarcosvncs) · [GitHub](https://github.com/MarcossVini) · [Email](mailto:marcos.vinisoft@gmail.com)

<br/>

![Profile views](https://komarev.com/ghpvc/?username=MarcossVini&color=24292f&style=flat-square&label=PROFILE+VIEWS)

</div>

---

## About

I'm a Software Engineer graduated from the **Federal University of Amazonas (UFAM)** and currently pursuing a postgraduate degree in **Data Science**.

My professional experience includes building web applications, REST APIs, ERP systems and integrations across different business domains. I work mainly with TypeScript, Node.js and React, with additional experience in Python, .NET, PHP and computer vision research.

I'm interested in backend engineering, software architecture, cloud infrastructure, distributed systems and data-driven solutions. I value maintainable code, clear domain boundaries, automated testing and continuous improvement.

---

## Activity

<div align="center">

<!-- GitHub contribution statistics -->
<img
  src="https://github-readme-stats.vercel.app/api?username=MarcossVini&show_icons=true&hide_title=true&hide_border=true&include_all_commits=true&count_private=true&rank_icon=github&bg_color=ffffff&title_color=24292f&text_color=57606a&icon_color=24292f"
  height="165"
  alt="GitHub statistics"
/>
<img
  src="https://github-readme-stats.vercel.app/api/top-langs/?username=MarcossVini&layout=compact&hide_border=true&langs_count=8&bg_color=ffffff&title_color=24292f&text_color=57606a"
  height="165"
  alt="Most used languages"
/>

<br/>

<img
  src="https://streak-stats.demolab.com?user=MarcossVini&hide_border=true&background=FFFFFF&ring=24292F&fire=24292F&currStreakLabel=24292F&sideLabels=57606A&currStreakNum=24292F&sideNums=24292F&dates=8C959F"
  width="70%"
  alt="GitHub contribution streak"
/>

<br/>

<img
  src="https://github-readme-activity-graph.vercel.app/graph?username=MarcossVini&bg_color=ffffff&color=24292f&line=57606a&point=24292f&area=true&area_color=eaeef2&hide_border=true"
  width="100%"
  alt="GitHub contribution activity graph"
/>

</div>

## Contribution map

<div align="center">

<!-- Generated automatically by .github/workflows/update-snake.yml -->
<img
  src="https://raw.githubusercontent.com/MarcossVini/MarcossVini/output/github-contribution-grid-snake.svg"
  width="100%"
  alt="GitHub contribution graph animation"
/>

</div>

---

## Technology

**Main stack**

<p>
  <img src="https://skillicons.dev/icons?i=ts,js,nodejs,react,nextjs,nestjs" alt="TypeScript, JavaScript, Node.js, React, Next.js and NestJS" />
</p>

**Data & infrastructure**

<p>
  <img src="https://skillicons.dev/icons?i=postgres,mysql,mongodb,redis,docker,aws,git,github,githubactions" alt="PostgreSQL, MySQL, MongoDB, Redis, Docker, AWS, Git, GitHub and GitHub Actions" />
</p>

**Additional experience**

<p>
  <img src="https://skillicons.dev/icons?i=python,php,laravel,dotnet,angular,vue,opencv,tensorflow" alt="Python, PHP, Laravel, .NET, Angular, Vue, OpenCV and TensorFlow" />
</p>

---

## Engineering interests

- Backend architecture and REST API design
- Distributed systems and service integration
- Relational and NoSQL database design
- Automated testing and code quality
- Cloud infrastructure and containerization
- Data engineering, computer vision and applied AI

---

## Education

**B.Sc. in Software Engineering**  
Federal University of Amazonas (UFAM) · 2018–2024

**Postgraduate studies in Data Science**  
UniCesumar · 2024–Present

---

<div align="center">

*Designing, building and improving software — one iteration at a time.*

</div>
'''

workflow = r'''name: Update contribution snake

on:
  schedule:
    - cron: "17 */12 * * *"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: Generate contribution snake
        uses: Platane/snk@v3
        with:
          github_user_name: MarcossVini
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Publish generated SVG files
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
'''

(base / "README.md").write_text(readme, encoding="utf-8")
(workflow_dir / "update-snake.yml").write_text(workflow, encoding="utf-8")

zip_path = Path("/mnt/data/marcos-github-profile-files.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for p in base.rglob("*"):
        if p.is_file():
            z.write(p, p.relative_to(base))

print("Created:")
print("/mnt/data/marcos-github-profile/README.md")
print("/mnt/data/marcos-github-profile/.github/workflows/update-snake.yml")
print(zip_path)
