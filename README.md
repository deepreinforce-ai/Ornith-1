# Ornith-1

<div align="center">
<img src=assets/ornith_logo.png width="65%"/>
</div>

<div align="center">

[![Ornith Blog](https://img.shields.io/badge/%F0%9F%A6%A2%EF%B8%8F%20Ornith%20Blog%20-FD8E5B)](https://deep-reinforce.com/ornith.html)

</div>

# Introduction


Aloha! 🌺 Today, we are releasing Ornith-1.0, a self-improving family of open-source models for agentic coding. 

Highlights: 

- **State-of-the-Art Coding Agents**: Available in 9B-Dense, 31B-Dense, 35B-MoE, and 397B-MoE (post-trained on top of Gemma 4 and Qwen 3.5), achieving state-of-the-art performance among open-source models of comparable size on coding benchmarks such as Terminal-Bench 2.1, SWE-Bench, NL2Repo and OpenClaw. 
- **Self-Improving Training Framework**:  Ornith-1.0 employs RL to learn to generate not only solution rollouts, but also the scallfold that drive those rollouts. By jointly optimizing the scaffold and the resulting solution, the model  discovers better search trajectories and generates higher-quality solutions. 
- **Licence**: MIT licensed, globally accessible, and free from regional limitations.

<img style="width: 100%; max-width: 900px;" src="assets/ornith_9b_eval.png" alt="Ornith 9B Benchmark Results" title="Ornith 9B Benchmark Results">

## Ornith 1.0 

Ornith-1.0 is released as a family of checkpoints — a **dense** 9B model and two **Mixture-of-Experts** models (35B, 397B), all post-trained for agentic coding, and each published in several precision / format variants (bf16, FP8, GGUF). This card covers the whole family: the benchmarks below compare every size, and the serving and usage recipes apply to all of them.

### Benchmarks

The table below merges the benchmark results of the full **Ornith-1.0** family (9B / 35B / 397B) into a single view. Each model is compared against the open-source and proprietary baselines reported in its respective model card.

<div style="font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,sans-serif;width:100%;margin:0 auto;padding:16px 0;overflow-x:auto">
<table style="min-width:1180px;border-collapse:collapse;font-size:12px">
<thead>
<tr>
<th style="padding:8px 8px;text-align:left;border-bottom:2px solid #FD8E5B;color:#FD8E5B"></th>
<th colspan="3" style="padding:8px 7px;text-align:center;font-weight:700;border-bottom:2px solid #FD8E5B;color:#FD8E5B;background:rgba(253,142,91,0.12);">Ornith-1.0 (ours)</th>
<th colspan="9" style="padding:8px 7px;text-align:center;font-weight:600;border-bottom:2px solid #FD8E5B;color:#FD8E5B;">Open-Source Baselines</th>
<th colspan="3" style="padding:8px 7px;text-align:center;font-weight:600;border-bottom:2px solid #FD8E5B;color:#FD8E5B;">Proprietary</th>
</tr>
<tr>
<th style="padding:8px 8px;text-align:left;border-bottom:2px solid #FD8E5B;color:#FD8E5B"></th>
<th style="padding:8px 6px;text-align:center;font-weight:700;border-bottom:2px solid #FD8E5B;color:#FD8E5B;background:rgba(253,142,91,0.12)">Ornith-1.0-9B</th>
<th style="padding:8px 6px;text-align:center;font-weight:700;border-bottom:2px solid #FD8E5B;color:#FD8E5B;background:rgba(253,142,91,0.12)">Ornith-1.0-35B</th>
<th style="padding:8px 6px;text-align:center;font-weight:700;border-bottom:2px solid #FD8E5B;color:#FD8E5B;background:rgba(253,142,91,0.12)">Ornith-1.0-397B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Qwen3.5-9B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Gemma4-12B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Qwen3.5-35B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Qwen3.6-35B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Gemma4-31B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Qwen3.5-397B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Minimax-M3-428B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">GLM-5.2-744B</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">DeepSeek-V4-Pro-1.6T</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Qwen3.7-Max</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Claude Opus 4.7</th>
<th style="padding:8px 6px;text-align:center;font-weight:500;border-bottom:2px solid #FD8E5B;color:#FD8E5B">Claude Opus 4.8</th>
</tr>
</thead>
<tbody>
<tr><td colspan="16" style="padding:8px 12px;font-weight:600;color:#FD8E5B;border-bottom:1px solid rgba(253,142,91,0.2);background:rgba(253,142,91,0.1)">Agentic Coding</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">Terminal-Bench 2.1 <sub><small>(Terminus-2)</small></sub></td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">43.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">64.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">77.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">21.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">21</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">41.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">52.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">42.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">53.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">64</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">81.0</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">64</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">73.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">70.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">85</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">Terminal-Bench 2.1 <sub><small>(Claude Code)</small></sub></td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">40.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">62.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">78.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">18.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">38.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">49.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">48.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">82.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">66.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">69.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">69.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">78.9</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">SWE-bench Verified</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">69.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">75.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">82.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">53.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">44.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">70</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">73.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">52</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">76.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">80.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">80.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">80.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">87.6</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">SWE-bench Pro</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">42.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">50.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">62.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">31.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">27.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">44.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">49.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">35.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">51.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">59</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">62.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">55.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">60.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">64.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">69.2</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">SWE-bench Multilingual</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">52</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">69.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">78.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">39.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">32.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">60.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">67.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">51.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">69.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">76.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">78.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">NL2Repo</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">27.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">34.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">48.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">16.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">10.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">20.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">29.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">15.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">36.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">42.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">48.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">47.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">69.7</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">Claw-eval Avg</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">63.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">69.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">77.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">53.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">32.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">65.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">68.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">48.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">70.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">75.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">65.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">78.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">SWE Atlas - QnA</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">17.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">37.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">41.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">9.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">13.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">15.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">20.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">37.9</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">27.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">40.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">48.8</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">SWE Atlas - RF</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">16.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">29.7</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">42.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">4.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">10.2</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">11.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">18.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">48.6</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">46.7</td></tr>
<tr><td style="padding:6px 8px;padding-left:16px;border-bottom:1px solid rgba(128,128,128,0.15);white-space:nowrap">SWE Atlas - TW</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">15.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">27.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15);font-weight:600;color:#FD8E5B;background:rgba(253,142,91,0.06)">39.1</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">4.4</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">9.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">13.3</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">18.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">30.8</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">38.5</td><td style="padding:6px 6px;text-align:center;border-bottom:1px solid rgba(128,128,128,0.15)">-</td></tr>
</tbody>
</table>
<p style="margin-top:12px;font-size:10px;opacity:0.7">
* Terminal-Bench 2.1 (Terminus-2): evaluated with the Harbor/Terminus-2 framework, parser=json, temperature=1.0, top_p=1.0, 128K context window. Each run uses a 4-hour timeout with 32 CPU cores and 48GB RAM, averaged over 5 runs. We adjust the Qwen chat template to keep training and inference consistent and modify Harbor to align with vLLM's reasoning_content key.<br/>
* Terminal-Bench 2.1 (Claude Code): evaluated with Claude Code 2.1.126, parser=json, temperature=1.0, top_p=1.0, max_new_tokens=131072, averaged over 5 runs (Qwen chat template likewise modified).<br/>
* SWE-bench Verified / Pro / Multilingual: OpenHands harness, temp=1.0, top_p=0.95, 256K context window.<br/>
* SWE Atlas QnA / RF / TW: mini-SWE-agent harness, temp=1.0, top_p=0.95, 128K context window, averaged over 5 runs.<br/>
* NL2Repo: temperature=1.0, top_p=1.0, 400K context, 48K output, anti-hacking filters.<br/>
* ClawEval: an agentic code benchmark over real-user task distributions; temp=0.6, 256K context.<br/>
* Each Ornith model is compared against the baselines reported in its own model card; cells marked <code>-</code> were not reported for that model.
</p>
</div>

## Quickstart

> **📝 NOTE**
>
> **Ornith-1.0** is a **reasoning model**: by default the assistant turn opens with a `<think> … </think>` block before the final answer. The serving recipes below enable a reasoning parser so the chain-of-thought is returned in a separate `reasoning_content` field, and a tool-call parser so the model's `<tool_call>` blocks are surfaced as OpenAI-style `tool_calls`.
>
> Serving Ornith-1.0 requires recent runtimes:
>
> - **Transformers** ≥ 5.8.1
> - **vLLM** ≥ 0.19.1
> - **SGLang** ≥ 0.5.9
>
> Recommended sampling parameters: `temperature=0.6`, `top_p=0.95`, `top_k=20` (use `temperature=1.0` to reproduce the reported benchmark setup).


### Serving Ornith-1.0

Ornith-1.0 ships as a dense **9B** model plus two **Mixture-of-Experts** models (**35B**, **397B**). All checkpoints expose the same OpenAI-compatible interface and support a **256K (262,144-token) context window**; the dense 9B fits on a single 80GB GPU, while the MoE checkpoints are sharded across a multi-GPU node with tensor parallelism. Each size is published in multiple precision / format variants:

| Checkpoint | Architecture | Format | Best for |
|---|---|---|---|
| [Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B) | Dense (~9B) | bf16 | Single-GPU serving & fine-tuning |
| [Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF) | Dense (~9B) | GGUF (quantized) | Local inference via llama.cpp / Ollama |
| [Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B) | MoE (35B) | bf16 | Full-precision multi-GPU serving |
| [Ornith-1.0-35B-FP8](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-FP8) | MoE (35B) | FP8 | ~Half the VRAM on FP8-capable GPUs |
| [Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF) | MoE (35B) | GGUF (quantized) | Local inference via llama.cpp / Ollama |
| [Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B) | MoE (397B) | bf16 | Full-precision serving on a multi-GPU node |
| [Ornith-1.0-397B-FP8](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B-FP8) | MoE (397B) | FP8 | Memory-efficient serving on FP8-capable GPUs |

The recipes below stand up an OpenAI-compatible server under the shared alias `Ornith-1.0`. Set `MODEL` to the checkpoint you want, and match `--tensor-parallel-size` / `--tp` to your GPU count.

#### vLLM

```bash
# Pick a checkpoint — dense 9B, or MoE 35B / 397B (append -FP8 for lower-VRAM serving):
MODEL=deepreinforce-ai/Ornith-1.0-397B

# MoE checkpoints (35B / 397B): shard across the node with tensor parallelism.
# Dense checkpoint (9B): fits on a single 80GB GPU — drop --tensor-parallel-size.
vllm serve $MODEL \
    --served-model-name Ornith-1.0 \
    --tensor-parallel-size 8 \
    --host 0.0.0.0 --port 8000 \
    --max-model-len 262144 \
    --gpu-memory-utilization 0.90 \
    --enable-prefix-caching \
    --enable-auto-tool-choice --tool-call-parser qwen3_xml \
    --reasoning-parser qwen3 \
    --trust-remote-code
```

#### SGLang

```bash
# Pick a checkpoint — dense 9B, or MoE 35B / 397B (append -FP8 for lower-VRAM serving):
MODEL=deepreinforce-ai/Ornith-1.0-397B

# MoE checkpoints (35B / 397B): shard with --tp ; dense 9B: drop --tp for a single GPU.
python -m sglang.launch_server \
    --model-path $MODEL \
    --served-model-name Ornith-1.0 \
    --tp 8 \
    --host 0.0.0.0 --port 8000 \
    --context-length 262144 \
    --mem-fraction-static 0.85 \
    --tool-call-parser qwen3_coder \
    --reasoning-parser qwen3
```

#### Hugging Face Transformers

For a quick local test (or to script offline generation), load the model directly with Transformers. Make sure you have a recent release installed — see the [Transformers installation guide](https://huggingface.co/docs/transformers/installation); Ornith-1.0 requires `transformers >= 5.8.1`. The dense 9B checkpoint is the easiest to run locally.

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model_name = "deepreinforce-ai/Ornith-1.0-9B"  # or -35B / -397B

tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(
    model_name,
    dtype="auto",
    device_map="auto",
)

messages = [
    {"role": "user", "content": "Write a Python function is_prime(n). Keep it short."}
]
text = tokenizer.apply_chat_template(
    messages,
    tokenize=False,
    add_generation_prompt=True,
)

inputs = tokenizer(text, return_tensors="pt").to(model.device)
generated = model.generate(
    **inputs,
    max_new_tokens=512,
    do_sample=True,
    temperature=0.6,
    top_p=0.95,
    top_k=20,
)
output_ids = generated[0][inputs.input_ids.shape[1]:]

# The reply contains a <think> ... </think> reasoning block followed by the answer.
content = tokenizer.decode(output_ids, skip_special_tokens=True)
print(content)
```

To split the reasoning trace from the final answer, parse on the `</think>` marker:

```python
text = tokenizer.decode(output_ids, skip_special_tokens=True)
if "</think>" in text:
    reasoning, answer = text.split("</think>", 1)
    reasoning = reasoning.replace("<think>", "").strip()
    answer = answer.strip()
else:
    reasoning, answer = "", text.strip()
```

### Using Ornith-1.0 via the Chat Completions API

Once a vLLM or SGLang server is running, talk to it with any OpenAI-compatible client.

#### Basic Usage

```python
from openai import OpenAI

client = OpenAI(
    base_url="http://localhost:8000/v1",
    api_key="EMPTY",  # any non-empty string works for a local server
)

response = client.chat.completions.create(
    model="Ornith-1.0",
    messages=[
        {"role": "user", "content": "Write a one-line Python lambda that squares a number."}
    ],
    temperature=0.6,
    top_p=0.95,
    max_tokens=1024,
)

message = response.choices[0].message
# reasoning_content holds the <think> trace; content holds the final answer.
print("reasoning:", getattr(message, "reasoning_content", None))
print("answer:", message.content)
```

You can also stream tokens, or hand the model tools — Ornith-1.0 emits well-formed function calls that the server parses into the standard `tool_calls` field:

```python
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get the current weather for a city",
            "parameters": {
                "type": "object",
                "properties": {"city": {"type": "string"}},
                "required": ["city"],
            },
        },
    }
]

response = client.chat.completions.create(
    model="Ornith-1.0",
    messages=[{"role": "user", "content": "What is the weather in Paris right now?"}],
    tools=tools,
    tool_choice="auto",
    temperature=0.6,
    max_tokens=2048,
)

tool_call = response.choices[0].message.tool_calls[0]
print(tool_call.function.name, tool_call.function.arguments)
# -> get_weather {"city": "Paris"}
```

You can point any OpenAI-compatible SDK (Python, Node.js, etc.) or `curl` at the same `/v1/chat/completions` endpoint.

## Agentic Usage

Ornith-1.0 excels in tool-calling and agentic coding capabilities.

### Agent Frameworks

Because Ornith-1.0 exposes an OpenAI-compatible endpoint with tool calling, it works out of the box with standard agent frameworks. Below is a minimal example that connects Ornith-1.0 to tools through an MCP server.

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url=os.getenv("OPENAI_BASE_URL", "http://localhost:8000/v1"),
    api_key=os.getenv("OPENAI_API_KEY", "EMPTY"),
)

tools = [
    {
        "type": "function",
        "function": {
            "name": "run_shell",
            "description": "Run a shell command and return its output.",
            "parameters": {
                "type": "object",
                "properties": {
                    "command": {"type": "string", "description": "The command to run"}
                },
                "required": ["command"],
            },
        },
    }
]

messages = [{"role": "user", "content": "List the Python files in the current directory."}]

response = client.chat.completions.create(
    model="Ornith-1.0",
    messages=messages,
    tools=tools,
    temperature=0.6,
    top_p=0.95,
)
print(response.choices[0].message)
```

**Examples of using Ornith with agent harness:**

#### Hermes Agent
```bash
# Hermes talks to any OpenAI-compatible endpoint — point it at your Ornith server.
export OPENAI_BASE_URL="http://localhost:8000/v1"
export OPENAI_API_KEY="EMPTY"
export MODEL="Ornith-1.0"
```

#### OpenHands
```bash
pip install openhands-ai

# OpenHands routes through LiteLLM; the "openai/" prefix selects the OpenAI-compatible path.
export LLM_MODEL="openai/Ornith-1.0"
export LLM_BASE_URL="http://localhost:8000/v1"
export LLM_API_KEY="EMPTY"

# Launch the CLI (or run the official OpenHands Docker image with the same env vars).
openhands
```

#### llama.cpp / Ollama
```bash
# Both runtimes load a GGUF build — available for the 9B and 35B checkpoints (swap -9B for -35B).

# llama.cpp — serve an OpenAI-compatible API on port 8000.
llama-server -hf deepreinforce-ai/Ornith-1.0-9B-GGUF --port 8000 -c 262144

# Ollama — pull and chat with the same GGUF straight from Hugging Face.
ollama run hf.co/deepreinforce-ai/Ornith-1.0-9B-GGUF
```

#### Unsloth Studio

```bash
pip install unsloth

# Load Ornith for fast local inference or fine-tuning (Python):
#   from unsloth import FastLanguageModel
#   model, tokenizer = FastLanguageModel.from_pretrained(
#       "deepreinforce-ai/Ornith-1.0-9B",
#       max_seq_length=262144,
#       load_in_4bit=True,
#   )
```


#### OpenClaw

```bash
# OpenClaw talks to any OpenAI-compatible endpoint — point it at your Ornith server.
export OPENAI_BASE_URL="http://localhost:8000/v1"
export OPENAI_API_KEY="EMPTY"
export OPENAI_MODEL="Ornith-1.0"
```


### Coding CLIs

Ornith-1.0 is optimized for terminal-based coding agents. Point any OpenAI-compatible coding CLI at your Ornith-1.0 endpoint (set `OPENAI_BASE_URL` and `OPENAI_API_KEY`) to understand large codebases, automate tedious work, and ship faster.

#### OpenCode
```bash
# Register your local Ornith endpoint as a provider in ~/.config/opencode/opencode.json:
#
# {
#   "$schema": "https://opencode.ai/config.json",
#   "provider": {
#     "ornith": {
#       "npm": "@ai-sdk/openai-compatible",
#       "name": "Ornith (local)",
#       "options": { "baseURL": "http://localhost:8000/v1", "apiKey": "EMPTY" },
#       "models": { "Ornith-1.0": { "name": "Ornith-1.0" } }
#     }
#   }
# }

opencode
```

### Citation

If you find our work helpful, feel free to give us a cite.

```bibtex
@misc{ornith-1.0,
    title = {{Ornith-1.0}: Agentic Coding, Open to All},
    url = {https://deep-reinforce.com/ornith_1_0.html},
    author = {{DeepReinforce Team}},
    year = {2026}
}
```