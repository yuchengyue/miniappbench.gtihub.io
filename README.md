# miniappbench.gtihub.io

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=IBM+Plex+Sans:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">

<div align="center">

<h1 style="font-size: 2.5rem; margin-bottom: 0.5rem;">MiniAppBench: Evaluating the Shift from Text to Interactive HTML Responses in LLM-Powered Assistants</h1>

<p style="font-size: 1.15rem; color: var(--color-text-light); font-weight: 300; max-width: 800px; margin: 1rem auto 2rem;">
Evaluating the Shift from Text to Interactive HTML Responses in LLM-Powered Assistants
</p>

<p style="font-size: 0.95rem; color: var(--color-text-light); margin-bottom: 2.5rem;">
<a href="#authors">Anonymous Authors</a> · <a href="#institution">Anonymous Institution</a>
</p>

<div class="update-notice" style="max-width: 750px; margin: 2rem auto; text-align: left;">
  <h3>📢 Latest Update — February 28, 2026</h3>
  <p style="margin-bottom: 1rem; line-height: 1.6;"><strong>Interactive Leaderboard Now Available!</strong> Test your models on MiniAppBench by submitting to our leaderboard. Simply provide your LLM API endpoint and let our evaluation framework automatically assess performance across 500 real-world tasks.</p>
  <div style="text-align: center; margin-top: 1.5rem;">
    <a href="https://huggingface.co/MiniAppBench" class="primary-cta">Submit to Leaderboard →</a>
  </div>
</div>

<div class="badge-row">
  <a href="#paper"><img src="https://img.shields.io/badge/Paper-arXiv-b31b1b?style=flat-square" alt="Paper"></a>
  <a href="https://huggingface.co/MiniAppBench"><img src="https://img.shields.io/badge/🏆-Leaderboard-1a1a2e?style=flat-square" alt="Leaderboard"></a>
  <a href="https://anonymous.4open.science/r/MiniAppBench"><img src="https://img.shields.io/badge/Code-GitHub-181717?style=flat-square&logo=github" alt="GitHub"></a>
  <a href="https://huggingface.co/MiniAppBench"><img src="https://img.shields.io/badge/🤗-Dataset-FFD21E?style=flat-square" alt="Dataset"></a>
  <a href="#x"><img src="https://img.shields.io/badge/X-000000?style=flat-square&logo=x&logoColor=white" alt="X"></a>
</div>

</div>

---

## Abstract

**Human-AI interaction is evolving from static text responses to dynamic, interactive applications.**

**MiniAppBench** is the first comprehensive benchmark designed to evaluate **principle-driven, interactive application generation**. While traditional benchmarks focus on static layouts or algorithmic snippets, MiniAppBench shifts the paradigm toward **MiniApps**—HTML-based applications that require both visual rendering and complex interaction logic.

<div align="center" style="margin: 25px 0;">
  <img src="./intro.png" alt="From Text to MiniApps" style="max-width: 500px; width: 100%; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);" />
  <p style="font-size: 0.9em; color: #666; line-height: 1.5; margin-top: 12px; max-width: 500px;"><em><strong>Figure 1.</strong> The shift from text to MINIAPPS. Unlike static text, MINIAPPS transforms abstract explanations into intuitive visualizations and unlocks actionable tasks (e.g., diet tracking) that were previously impossible.</em></p>
</div>

### Key Highlights

- 🌍 **Real-World Scale:** Distilled from 10M+ generations
- 📊 **500 Diverse Tasks:** Across 6 domains
- 🤖 **MiniAppEval Framework:** Agentic browser automation
- 📏 **Multi-Dimensional:** Intention, Static, Dynamic scoring
- 🔬 **High Alignment:** Pearson r > 0.85 with humans

---

## Benchmark Construction and Statistics

<div align="center">
  <img src="./pipeline.png" alt="MiniAppBench Construction Pipeline" style="max-width: 95%; border-radius: 8px; margin-bottom: 20px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);" />
  <p><em>Figure 1: MiniAppBench data construction pipeline from production application (10M+ generations) to curated evaluation benchmark</em></p>
</div>

### Task Distribution by Domain

<div align="center">

| Domain | Tasks | Description |
|:-------|:-----:|:------------|
| **🔬 Science** | 187 | Simulators and virtual laboratories for chemistry, biology, physics, and geometry |
| **🎮 Games** | 121 | Logic puzzles, projectile motion games, systemic simulations, and casual/card games |
| **🛠️ Tools** | 57 | Practical utilities including schedulers, creative editors, and computational tools |
| **📊 Visualization** | 56 | SVG-based graphics, statistical charts, and interactive generative art |
| **📚 Humanities** | 47 | Interactive platforms for skill acquisition, concept deconstruction, and cultural study |
| **💚 Lifestyle** | 32 | Health and wellness trackers, interactive toys, and roleplay-based applications |
| **Total** | **500** | Comprehensive coverage of interactive application scenarios |

</div>

---

## Methodology: MiniAppEval

Unlike benchmarks with a single "ground truth," **MiniAppEval** addresses the open-ended nature of interactive applications through an **Agentic Framework** (powered by Gemini 3 Pro) that processes **four core inputs**: (i) the **user query $q_i$**, (ii) a structured **evaluation reference $r_i$**, (iii) the **generated source code**, and (iv) a **live, interactable MiniApp instance**.

1.  **Exploration:** An LLM-based agent interacts with the live MiniApp in a browser (clicking, dragging, typing).
2.  **Observation:** The system captures a comprehensive **interaction trajectory**, recording DOM states, console logs, and the underlying source code, providing the raw evidence required for deep analysis.
3.  **Grading:** The agent scores the MiniApp based on the collected evidence. The evaluation reference $r_i$ informs the inspection strategy but does not serve as a rigid oracle.
    *   **Intention Alignment:** Verifies if the MiniApp fulfills the high-level user goal (e.g., representing core dynamics like energy conservation in a physics simulation).
    *   **Static Quality:** Evaluates structural and syntactic correctness without execution, verifying the presence of required elements, code organization, and adherence to accessibility standards.
    *   **Dynamic Logic:** Assesses runtime behavior through trajectories, focusing on **Sequential Logic** (consistent state transitions and interaction flow) and **Robustness** (graceful handling of edge cases and adversarial inputs).

---

## Experimental Results

We evaluated **15 state-of-the-art LLMs** across 500 tasks, measuring pass rates by difficulty, domain, and overall performance.

### Performance Leaderboard

<div style="overflow-x: auto;">
<table style="width: 100%; border-collapse: collapse; font-size: 0.9em;">
  <thead>
    <tr style="border-bottom: 2px solid #333;">
      <th style="text-align: left; padding: 8px;">Model</th>
      <th style="text-align: center; padding: 8px;"><strong>Avg (%)</strong></th>
      <th style="text-align: center; padding: 8px;">Easy</th>
      <th style="text-align: center; padding: 8px;">Mid</th>
      <th style="text-align: center; padding: 8px;">Hard</th>
      <th style="text-align: center; padding: 8px;">Games</th>
      <th style="text-align: center; padding: 8px;">Science</th>
      <th style="text-align: center; padding: 8px;">Tools</th>
      <th style="text-align: center; padding: 8px;">Humanities</th>
      <th style="text-align: center; padding: 8px;">Viz</th>
      <th style="text-align: center; padding: 8px;">Lifestyle</th>
      <th style="text-align: center; padding: 8px;">Tokens</th>
      <th style="text-align: center; padding: 8px;">Time(s)</th>
    </tr>
  </thead>
  <tbody>
    <!-- Open-Source Models -->
    <tr style="background-color: #fffacd;">
      <td colspan="13" style="text-align: center; padding: 8px; font-style: italic;"><em>Open-Source Large Language Models</em></td>
    </tr>
    <tr>
      <td style="padding: 8px;">Qwen3-32B</td>
      <td style="text-align: center; padding: 8px;">0.66</td>
      <td style="text-align: center; padding: 8px;">1.59</td>
      <td style="text-align: center; padding: 8px;">0.55</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.57</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">2.04</td>
      <td style="text-align: center; padding: 8px;">3.70</td>
      <td style="text-align: center; padding: 8px;">3,470.68</td>
      <td style="text-align: center; padding: 8px;">22.16</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Qwen3-235B-A22B</td>
      <td style="text-align: center; padding: 8px;">2.88</td>
      <td style="text-align: center; padding: 8px;">6.43</td>
      <td style="text-align: center; padding: 8px;">2.35</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.93</td>
      <td style="text-align: center; padding: 8px;">0.60</td>
      <td style="text-align: center; padding: 8px;">4.00</td>
      <td style="text-align: center; padding: 8px;">4.88</td>
      <td style="text-align: center; padding: 8px;">7.27</td>
      <td style="text-align: center; padding: 8px;">10.34</td>
      <td style="text-align: center; padding: 8px;">4,068.27</td>
      <td style="text-align: center; padding: 8px;">49.55</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Qwen3-Coder-480B-A35B-Instruct</td>
      <td style="text-align: center; padding: 8px;">1.83</td>
      <td style="text-align: center; padding: 8px;">6.06</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">9.43</td>
      <td style="text-align: center; padding: 8px;">11.11</td>
      <td style="text-align: center; padding: 8px;">2,324.83</td>
      <td style="text-align: center; padding: 8px;">25.04</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Kimi-K2-Instruct</td>
      <td style="text-align: center; padding: 8px;">6.19</td>
      <td style="text-align: center; padding: 8px;">14.17</td>
      <td style="text-align: center; padding: 8px;">5.03</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">3.77</td>
      <td style="text-align: center; padding: 8px;">3.11</td>
      <td style="text-align: center; padding: 8px;">4.08</td>
      <td style="text-align: center; padding: 8px;">4.88</td>
      <td style="text-align: center; padding: 8px;">17.65</td>
      <td style="text-align: center; padding: 8px;">18.52</td>
      <td style="text-align: center; padding: 8px;">3,435.97</td>
      <td style="text-align: center; padding: 8px;">46.76</td>
    </tr>
    <tr>
      <td style="padding: 8px;">GLM-4.5-Air</td>
      <td style="text-align: center; padding: 8px;">7.09</td>
      <td style="text-align: center; padding: 8px;">17.60</td>
      <td style="text-align: center; padding: 8px;">4.07</td>
      <td style="text-align: center; padding: 8px;">1.44</td>
      <td style="text-align: center; padding: 8px;">5.66</td>
      <td style="text-align: center; padding: 8px;">4.27</td>
      <td style="text-align: center; padding: 8px;">6.98</td>
      <td style="text-align: center; padding: 8px;">7.32</td>
      <td style="text-align: center; padding: 8px;">16.98</td>
      <td style="text-align: center; padding: 8px;">10.34</td>
      <td style="text-align: center; padding: 8px;">7,110.65</td>
      <td style="text-align: center; padding: 8px;">58.94</td>
    </tr>
    <tr>
      <td style="padding: 8px;"><strong>GLM-4.7</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>18.31</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>36.30</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>15.06</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>4.41</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>12.50</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>10.49</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>20.00</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>17.07</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>35.19</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>48.39</strong></td>
      <td style="text-align: center; padding: 8px;">8,936.88</td>
      <td style="text-align: center; padding: 8px;">55.58</td>
    </tr>
    <!-- Closed-Source Models -->
    <tr style="background-color: #e6f2ff;">
      <td colspan="13" style="text-align: center; padding: 8px; font-style: italic;"><em>Closed-Source Large Language Models</em></td>
    </tr>
    <tr>
      <td style="padding: 8px;">Hunyuan-Turbos-Latest</td>
      <td style="text-align: center; padding: 8px;">2.32</td>
      <td style="text-align: center; padding: 8px;">6.32</td>
      <td style="text-align: center; padding: 8px;">0.87</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">3.03</td>
      <td style="text-align: center; padding: 8px;">0.00</td>
      <td style="text-align: center; padding: 8px;">13.51</td>
      <td style="text-align: center; padding: 8px;">3.57</td>
      <td style="text-align: center; padding: 8px;">3,727.55</td>
      <td style="text-align: center; padding: 8px;">132.67</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Mimo-V2-Flash</td>
      <td style="text-align: center; padding: 8px;">12.48</td>
      <td style="text-align: center; padding: 8px;">28.68</td>
      <td style="text-align: center; padding: 8px;">8.33</td>
      <td style="text-align: center; padding: 8px;">2.22</td>
      <td style="text-align: center; padding: 8px;">13.46</td>
      <td style="text-align: center; padding: 8px;">6.02</td>
      <td style="text-align: center; padding: 8px;">10.87</td>
      <td style="text-align: center; padding: 8px;">11.63</td>
      <td style="text-align: center; padding: 8px;">23.53</td>
      <td style="text-align: center; padding: 8px;">36.36</td>
      <td style="text-align: center; padding: 8px;">5,109.82</td>
      <td style="text-align: center; padding: 8px;">37.98</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Grok-4.1-Fast-Reasoning</td>
      <td style="text-align: center; padding: 8px;">13.77</td>
      <td style="text-align: center; padding: 8px;">29.66</td>
      <td style="text-align: center; padding: 8px;">12.12</td>
      <td style="text-align: center; padding: 8px;">2.19</td>
      <td style="text-align: center; padding: 8px;">8.41</td>
      <td style="text-align: center; padding: 8px;">6.58</td>
      <td style="text-align: center; padding: 8px;">20.00</td>
      <td style="text-align: center; padding: 8px;">17.50</td>
      <td style="text-align: center; padding: 8px;">32.65</td>
      <td style="text-align: center; padding: 8px;">25.93</td>
      <td style="text-align: center; padding: 8px;">9,010.00</td>
      <td style="text-align: center; padding: 8px;">75.62</td>
    </tr>
    <tr>
      <td style="padding: 8px;">MiniMax-M2.1</td>
      <td style="text-align: center; padding: 8px;">17.12</td>
      <td style="text-align: center; padding: 8px;">31.46</td>
      <td style="text-align: center; padding: 8px;">15.62</td>
      <td style="text-align: center; padding: 8px;">7.08</td>
      <td style="text-align: center; padding: 8px;">16.25</td>
      <td style="text-align: center; padding: 8px;">12.50</td>
      <td style="text-align: center; padding: 8px;">23.33</td>
      <td style="text-align: center; padding: 8px;">20.00</td>
      <td style="text-align: center; padding: 8px;">27.27</td>
      <td style="text-align: center; padding: 8px;">19.23</td>
      <td style="text-align: center; padding: 8px;">8,881.57</td>
      <td style="text-align: center; padding: 8px;">118.32</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Gemini-3-Flash</td>
      <td style="text-align: center; padding: 8px;">17.62</td>
      <td style="text-align: center; padding: 8px;">32.76</td>
      <td style="text-align: center; padding: 8px;">16.89</td>
      <td style="text-align: center; padding: 8px;">4.10</td>
      <td style="text-align: center; padding: 8px;">14.95</td>
      <td style="text-align: center; padding: 8px;">10.60</td>
      <td style="text-align: center; padding: 8px;">17.95</td>
      <td style="text-align: center; padding: 8px;">18.18</td>
      <td style="text-align: center; padding: 8px;">30.61</td>
      <td style="text-align: center; padding: 8px;">41.38</td>
      <td style="text-align: center; padding: 8px;">6,563.28</td>
      <td style="text-align: center; padding: 8px;">50.56</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Gemini-3-Pro-Preview</td>
      <td style="text-align: center; padding: 8px;">27.52</td>
      <td style="text-align: center; padding: 8px;">61.98</td>
      <td style="text-align: center; padding: 8px;">20.83</td>
      <td style="text-align: center; padding: 8px;">1.71</td>
      <td style="text-align: center; padding: 8px;">26.74</td>
      <td style="text-align: center; padding: 8px;">19.11</td>
      <td style="text-align: center; padding: 8px;">13.64</td>
      <td style="text-align: center; padding: 8px;">28.57</td>
      <td style="text-align: center; padding: 8px;">52.00</td>
      <td style="text-align: center; padding: 8px;">55.56</td>
      <td style="text-align: center; padding: 8px;">5,815.14</td>
      <td style="text-align: center; padding: 8px;">80.80</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Claude-Sonnet-4.5</td>
      <td style="text-align: center; padding: 8px;">26.36</td>
      <td style="text-align: center; padding: 8px;">68.22</td>
      <td style="text-align: center; padding: 8px;">14.86</td>
      <td style="text-align: center; padding: 8px;">1.79</td>
      <td style="text-align: center; padding: 8px;">16.13</td>
      <td style="text-align: center; padding: 8px;">22.30</td>
      <td style="text-align: center; padding: 8px;">29.27</td>
      <td style="text-align: center; padding: 8px;">23.81</td>
      <td style="text-align: center; padding: 8px;">47.73</td>
      <td style="text-align: center; padding: 8px;">44.83</td>
      <td style="text-align: center; padding: 8px;">8,586.84</td>
      <td style="text-align: center; padding: 8px;">91.43</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Claude-Opus-4.5</td>
      <td style="text-align: center; padding: 8px;">41.14</td>
      <td style="text-align: center; padding: 8px;">59.09</td>
      <td style="text-align: center; padding: 8px;">41.18</td>
      <td style="text-align: center; padding: 8px;">22.33</td>
      <td style="text-align: center; padding: 8px;">37.18</td>
      <td style="text-align: center; padding: 8px;">34.59</td>
      <td style="text-align: center; padding: 8px;">47.50</td>
      <td style="text-align: center; padding: 8px;">35.71</td>
      <td style="text-align: center; padding: 8px;">57.45</td>
      <td style="text-align: center; padding: 8px;">56.52</td>
      <td style="text-align: center; padding: 8px;">13,152.75</td>
      <td style="text-align: center; padding: 8px;">166.66</td>
    </tr>
    <tr>
      <td style="padding: 8px;">GPT-5.1</td>
      <td style="text-align: center; padding: 8px;">32.00</td>
      <td style="text-align: center; padding: 8px;">74.71</td>
      <td style="text-align: center; padding: 8px;">21.37</td>
      <td style="text-align: center; padding: 8px;">3.49</td>
      <td style="text-align: center; padding: 8px;">24.14</td>
      <td style="text-align: center; padding: 8px;">18.10</td>
      <td style="text-align: center; padding: 8px;">33.33</td>
      <td style="text-align: center; padding: 8px;">45.83</td>
      <td style="text-align: center; padding: 8px;">57.78</td>
      <td style="text-align: center; padding: 8px;">64.71</td>
      <td style="text-align: center; padding: 8px;">11,256.15</td>
      <td style="text-align: center; padding: 8px;">154.09</td>
    </tr>
    <tr>
      <td style="padding: 8px;"><strong>GPT-5.2</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>45.46</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>69.77</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>43.08</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>18.64</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>40.32</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>50.38</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>50.17</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>45.45</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>75.00</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>82.35</strong></td>
      <td style="text-align: center; padding: 8px;">10,793.68</td>
      <td style="text-align: center; padding: 8px;">169.60</td>
    </tr>
    <!-- Average -->
    <tr style="border-top: 2px solid #333; background-color: #f0f0f0;">
      <td style="padding: 8px;"><strong>Average</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>17.05</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>34.05</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>13.89</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>4.34</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>14.71</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>11.64</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>18.07</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>17.55</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>31.63</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>33.30</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>—</strong></td>
      <td style="text-align: center; padding: 8px;"><strong>—</strong></td>
    </tr>
  </tbody>
</table>
</div>






### Key Findings

- **Performance Gaps**: Best closed-source model (GPT-5.2) achieves 45.46%, while best open-source (GLM-4.7) reaches 18.31%
- **Difficulty Scaling**: Pass rate drops from 34.05% (Easy) → 13.89% (Mid) → 4.34% (Hard)
- **Domain Variance**: Lifestyle (33.30%) easiest, Science (11.64%) hardest
- **Validation**: Pearson correlation with human judgment r > 0.85

---

## 🏆 Leaderboard

### How to Submit Your Model

We offer **two ways** to evaluate your model on MiniAppBench:

#### Option 1: Local Evaluation (Recommended for Development)

```bash
# Clone the repository
git clone https://anonymous.4open.science/r/MiniAppBench
cd MiniAppBench

# Install dependencies
pip install -r requirements.txt
playwright install chromium

# Run evaluation on your model
python -m examples.pipeline \
  --query-file data/query.json \
  --model-name "your-model-name" \
  --api-key "your-api-key" \
  --batch "0-499" \
  --parallel \
  --concurrency 5

# Results will be saved to generated_miniapps/logs/
```

**Local evaluation allows you to:**
- 🔍 Debug individual test cases
- ⚡ Iterate quickly during development
- 📊 Analyze detailed error logs
- 🎨 Preview generated MiniApps in browser

---

#### Option 2: Submit to Official Leaderboard

To have your results **verified and displayed** on the official leaderboard:

**Step 1: Prepare Your Submission**

Fill out the submission form with:
- **Model Name** (e.g., "GPT-4.5-Turbo", "Claude-Sonnet-4")
- **Organization/Team** (Optional for anonymous submissions)
- **API Endpoint** (OpenAI-compatible format)
- **API Key** (Will be kept confidential and deleted after evaluation)
- **Model Configuration** (temperature, max_tokens, etc.)

**Step 2: Automated Evaluation**

Our evaluation servers will:
1. Run all 500 benchmark tasks on your model
2. Execute MiniAppEval agent testing in isolated browsers
3. Compute multi-dimensional scores (Intention, Static, Dynamic)
4. Generate detailed error analysis and trajectory logs

**Step 3: Review & Publication**

- Evaluation typically completes within **6-12 hours**
- You'll receive a detailed report via email
- Scores will be published on the leaderboard after review
- Anonymized results available during submission period

**🚀 [Submit Your Model to Leaderboard](https://huggingface.co/spaces/anonymous/miniappbench-leaderboard)**

---

### Submission Guidelines

**API Requirements:**
- ✅ **OpenAI-compatible endpoint** (`/v1/chat/completions`)
- ✅ **Concurrent QPS ≥ 10** (parallel evaluation to reduce wait time; lower QPS significantly slows evaluation)
- ✅ Supports system/user message roles
- ✅ Returns complete HTML/CSS/JS in single response

**Evaluation Policy:**
- Free tier: 1 submission per week
- Academic researchers: Contact us for unlimited access
- APIs used **only for evaluation** and **deleted immediately after**

📧 **Questions?** miniappbench@anonymous.org

---

## Citation

```bibtex
@article{miniappbench2026,
  title={MiniAppBench: Evaluating the Shift from Text to Interactive HTML Responses in LLM-Powered Assistants},
  author={Anonymous Authors},
  journal={International Conference on Machine Learning (ICML)},
  year={2026}
}
```

---


<div align="center">

**MiniAppBench** — *Advancing the Frontier of Interactive Human-AI Collaboration*

[Paper](#paper) · [Leaderboard](#leaderboard) · [GitHub](https://github.com/anonymous/MiniAppBench) · [Hugging Face](https://huggingface.co/spaces/anonymous/miniappbench-leaderboard)

<p style="margin-top: 30px; color: #666;">
Total Visitors: <img src="https://visitor-badge.laobi.icu/badge?page_id=miniappbench" alt="Visitors"> ·
Last Updated: 2026-02-28
</p>

</div>
