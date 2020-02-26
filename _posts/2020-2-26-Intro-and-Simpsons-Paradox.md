---
layout: post
title: Welcome to Esoteria!
---
This blog will be data science-centric, but I will often incorporate topics and concepts from a wide gamut of fields –– mathematics, physics, statistics, computer science, machine learning, AI, cryptography, game theory, and more. My background is broadly cross-sectional, and I know a number of not-even-that-funny-domain-specific-jokes, so let it not be said that you were not warned!

Let's kick off the blog with a discussion on [**Simpson's Paradox**](https://en.wikipedia.org/wiki/Simpson's_paradox), a statistical phenomenon where trends in subpopulations disappear or reverse in the aggregate. I'll illustrate this paradox with two classical examples (batting averages year-over-year and a 1970s study on UC Berkeley's admissions of women), and then highlight an instance where it showed up in my analysis of a dataset.

## ACT/SAT, Part I
The ACT/SAT score dataset is a popular introductory dataset. It tabulates average SAT and ACT scores, by subject, on a state-by-state and year-by-year basis. Cursory exploration of the correlations of the dataset reveals that state-averaged SAT scores correlate negatively with state-averaged ACT scores, and vice versa. Put another way, if a state performs well on the SAT, we might expect it to perform poorly on the ACT.


![](/images/scatter4.svg)


Here we have average SAT and ACT scores scattered by state, and an ordinary linear regression with its associated 95% confidence interval (exercise for the reader: why does the 95% confidence band appear nonlinear?). This plot flies in the face of conventional wisdom –– some states are known for having good education, some are known for having bad education, and it is not an unreasonable belief that states with better education should perform better on both exams. I would further assert that  a top scoring SAT student should do relatively well on the ACT, and so this trend should manifest on an individual basis. So why is it that we do not observe this? **If our prior beliefs are true, why does this trend disappear in the aggregate?**

Obviously this ties in to Simpson's Paradox (else I wouldn't be writing about it!), but let us humor some alternative explanations. A very plausible hypothesis is that my prior beliefs are simply wrong. Maybe the educational apparatus of the state has no impact on the results of standardized tests (this would be somewhat alarming if true, since some states explicitly use the SAT or ACT as their state-wide standardized test).

Alternatively, it is possible that SAT-taking skill does not transfer to ACT-testing skill. The ACT organization itself asserts that the ACT is "a curriculum-based achievement test, measuring what a student has learned in school", and that the SAT "is more of an aptitude test, testing reasoning and verbal abilities". In light of this assertion, one can hypothesize that the ACT and SAT test fundamentally different and divergent skillsets, so states and students that prepare for one test understandably perform worse on the other.
## Baseball batting averages
The tables in the next two sections are taken from the Wikipedia article on Simpson's Paradox.

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


In the data above, David Justice has higher yearly batting averages, but when taken together Derek Jeter's batting average is significantly higher over the same time period. Here the effect arises because of the discrepancy of sample sizes –– if we compare Derek Jeter's 1996 batting average to David Justice's 1995, it becomes manifestly obvious that Derek Jeter is the better batter, but since we compare chronological samples of different statistical significance, we can observe a "paradoxical" result.

## UC Berkeley Admission Rates

[Sex Bias in Graduate Admissions: Data from Berkeley](https://homepage.stat.uiowa.edu/~mbognar/1030/Bickel-Berkeley.pdf) is a classic study on gender bias in admissions decisions. Looking at the admission rates for Fall 1973, researchers found the following:
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-cly1{text-align:left;vertical-align:middle}
.tg .tg-yla0{font-weight:bold;text-align:left;vertical-align:middle}
</style>
<table class="tg">
  <tr>
    <th class="tg-cly1" rowspan="2"></th>
    <th class="tg-cly1" colspan="2">Men</th>
    <th class="tg-cly1" colspan="2">Women</th>
  </tr>
  <tr>
    <td class="tg-cly1">Applicants</td>
    <td class="tg-cly1">Admitted</td>
    <td class="tg-cly1">Applicants</td>
    <td class="tg-cly1">Admitted</td>
  </tr>
  <tr>
    <td class="tg-cly1">Total</td>
    <td class="tg-cly1">8442</td>
    <td class="tg-yla0">44%</td>
    <td class="tg-cly1">4321</td>
    <td class="tg-cly1">35%</td>
  </tr>
</table>

A naive analysis would conclude that the admissions process was biased against women. However, when the researchers broke down admission rates by department, they found the following:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-9wq8{border-color:inherit;text-align:center;vertical-align:middle}
.tg .tg-9j3s{font-weight:bold;border-color:inherit;text-align:right;vertical-align:middle}
.tg .tg-c3ow{border-color:inherit;text-align:center;vertical-align:top}
.tg .tg-wk3d{font-weight:bold;font-style:italic;border-color:inherit;text-align:right;vertical-align:middle}
.tg .tg-yz93{border-color:inherit;text-align:right;vertical-align:middle}
.tg .tg-3osn{font-weight:bold;font-style:italic;border-color:inherit;text-align:right;vertical-align:top}
.tg .tg-dvpl{border-color:inherit;text-align:right;vertical-align:top}
.tg .tg-6ic8{font-weight:bold;border-color:inherit;text-align:right;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-9wq8" rowspan="2">Department</th>
    <th class="tg-9wq8" colspan="2">Men</th>
    <th class="tg-9wq8" colspan="2">Women</th>
  </tr>
  <tr>
    <td class="tg-9wq8">Applicants</td>
    <td class="tg-9wq8">Admitted</td>
    <td class="tg-9wq8">Applicants</td>
    <td class="tg-9wq8">Admitted</td>
  </tr>
  <tr>
    <td class="tg-9wq8"><br>A</td>
    <td class="tg-wk3d">825</td>
    <td class="tg-yz93">62%</td>
    <td class="tg-yz93">108</td>
    <td class="tg-9j3s">82%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">B</td>
    <td class="tg-3osn">560</td>
    <td class="tg-dvpl">63%</td>
    <td class="tg-dvpl">25</td>
    <td class="tg-6ic8">68%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">C</td>
    <td class="tg-dvpl">325</td>
    <td class="tg-6ic8">37%</td>
    <td class="tg-3osn">593</td>
    <td class="tg-dvpl">34%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">D</td>
    <td class="tg-dvpl">417</td>
    <td class="tg-dvpl">33%</td>
    <td class="tg-dvpl">375</td>
    <td class="tg-6ic8">35%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">E</td>
    <td class="tg-dvpl">191</td>
    <td class="tg-6ic8">28%</td>
    <td class="tg-3osn">393</td>
    <td class="tg-dvpl">24%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">F</td>
    <td class="tg-dvpl">373</td>
    <td class="tg-dvpl">6%</td>
    <td class="tg-dvpl">341</td>
    <td class="tg-6ic8">7%</td>
  </tr>
</table>

Tabulated here are the data from Berkeley's six largest departments. The top two departments
by number of applicants for each gender are italicised.

The study concluded that more departments actually admitted women at a higher rate than men. What ultimately brought women's admission rate down was the fact that women tended to apply to more selective departments. A large number of men were admitted to the largest, least selective departments, inflating their overall admittance percentage. Thus, even if most departments admit women at a higher rate than men, it is possible for women's overall admittance rate to be lower!


## ACT/SAT, Redux
Now let us return to the SAT/ACT data. We've implied that Simpson's Paradox is involved here, so without further ado:


![](/images/scatter5.svg)

Each state is colored by the relative difference in participation rate of SAT/ACT. Red points are states where most students take the SAT; blue points are states where most take the ACT. Our data separates itself neatly into distinct populations, each featuring a positive correlation between SAT and ACT scores.


Thus, for this dataset, we have resolved Simpson's Paradox. Our spurious negative correlation is the result of a selection bias. Most students choose to take either the SAT or the ACT (but not both), depending primarily on where they live. Since it costs resources (money, time, energy, etc.) to prepare for a non-mandatory standardized test, only those that are better equipped to take the alterative do so. Thus, any low-participation average test score is in some sense sampled from the tail of the "true" score distribution, the hypothetical alternate-test performance of every student in the state, and higher than what a more representative sample would show.

## Simpson's Paradox, in math:
Having
\[\frac ab > \frac cd\]
\[\frac ef > \frac gh\]
does not imply that
\begin{align}
\frac{a + e}{b + f} > \frac{c +g}{d + h}
\end{align}
