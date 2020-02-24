---
layout: post
title: Welcome to Esoteria, a personal blog by Nicholas Jin!
---
This blog is focused on data science, but I will often incorporate topics and concepts from a wide gamut of fields –– mathematics, physics, statistics, computer science, machine learning, AI, cryptography, game theory, and more. My background is broadly cross-sectional, and I know a number of very-specific and not-even-that-funny-domain-specific-jokes, so let it not be said that you were not warned!

# Learning with a toy dataset
Almost every data scientist at some point works through some subset of notable toy datasets (some sort of housing price dataset, the iris dataset, the titanic dataset –– the list goes on). Our inaugural post will feature the ACT/SAT score dataset, which is a collection of yearly average state-wide standardized test scores, further subdivided by subject. The dataset also includes the participation rate (defined variously as the percentage of graduating seniors that took the exam, or pinned to 100% if it was state-mandated).

# Simpson's Paradox
[**Simpson's Paradox**](https://en.wikipedia.org/wiki/Simpson's_paradox) is a statistical phenomenon where trends in subpopulations disappear in the aggregate. This can be illustrated with a number of examples, so we'll focus on a simple example (batting averages year-over-year) and the canonical example, a 1970s study on UC Berkeley's admissions of women.
## Baseball batting averages
<!-- | Batter \ Year   | 1995           | 1996  | |
| ------------- |:-------------:| -----:||
| Derek Jeter      | 12/48 \| .250 | $1600 ||
| David Justice      | 104/411 \| .253 | centered      |   $12 || -->


<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-wp8o{border-color:#000000;text-align:center;vertical-align:top}
.tg .tg-mcqj{font-weight:bold;border-color:#000000;text-align:left;vertical-align:top}
.tg .tg-73oq{border-color:#000000;text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-mcqj">Batter \ Year</th>
    <th class="tg-mcqj" colspan="2">1995</th>
    <th class="tg-mcqj" colspan="2">1996</th>
    <th class="tg-mcqj" colspan="2">Combined</th>
  </tr>
  <tr>
    <td class="tg-73oq">Derek Jeter</td>
    <td class="tg-wp8o">12/48</td>
    <td class="tg-73oq">.250</td>
    <td class="tg-73oq">183/582</td>
    <td class="tg-73oq">.314</td>
    <td class="tg-73oq">195/630</td>
    <td class="tg-73oq"><span style="font-weight:bold">.310</span><br></td>
  </tr>
  <tr>
    <td class="tg-73oq">David Justice</td>
    <td class="tg-wp8o">104/411</td>
    <td class="tg-73oq"><span style="font-weight:bold">.253</span></td>
    <td class="tg-73oq">45/140</td>
    <td class="tg-73oq"><span style="font-weight:bold">.321</span></td>
    <td class="tg-73oq">149/551</td>
    <td class="tg-73oq">.270</td>
  </tr>
</table>












<!-- <table>
  <tr>
    <th>Batter \ Year</th>
    <th colspan="2">1995</th>
    <th colspan="2">1996</th>
    <th colspan="2">Combined</th>
  </tr>
  <tr>
    <td>Derek Jeter</td>
    <td>12/48</td>
    <td>.250</td>
    <td>183/582</td>
    <td>.314</td>
    <td>195/630</td>
    <td><span style="font-weight:bold">.310</span><br></td>
  </tr>
  <tr>
    <td>David Justice</td>
    <td>104/411</td>
    <td><span style="font-weight:bold">.253</span></td>
    <td>45/140</td>
    <td><span style="font-weight:bold">.321</span></td>
    <td>149/551</td>
    <td>.270</td>
  </tr>
</table> -->
In the data above, David Justice has higher yearly batting averages, but when taken together Derek Jeter's batting average is significantly higher over the same time period.

## [Sex Bias in Graduate Admissions: Data from Berkeley](https://homepage.stat.uiowa.edu/~mbognar/1030/Bickel-Berkeley.pdf)

## ACT/SAT
We previously remarked upon the fact that state-averaged SAT scores correlate negatively with state-averaged ACT scores. An uncautious analysis might conclude that could lead to spurious conclusions
Note that there is also a selection bias in this dataset. Most students choose to take either the SAT or the ACT, depending primarily on where they live. Since it costs resources (money, time, energy) to prepare for a non-mandatory standardized test, only those
