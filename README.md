# Capstone Project 2025-2026

### **Basic Details**

**Project Title:** Of Bytes and Watts: Regulatory Safeguards of Powering AI Infrastructure

**Research Question:** Using network modelling of international energy trade and causal analysis of data centre regulation frameworks to inform policy insights that aim to manage data centre growth

**Authored By:** Amara Jane Otero Salgado, Zaki Zainudin, Dhruv Banerjee

---

### **Links**

- [Final Report](https://github.com/Dhruv-baner/capstone_edf_2026/blob/main/report_edf_2026.pdf): The full report containing our literature review, methodology, and analysis (download to read)

- [Policy Database](https://github.com/Dhruv-baner/capstone_edf_2026/blob/main/policy_database.csv): Policies across Europe that directly or indirectly affect data centres. This includes planning or zoning frameworks, general or specific energy efficiency laws, and incentives (such as growth zones)

- [Notable Policies in Europe](https://github.com/Dhruv-baner/capstone_edf_2026/blob/main/regulation_notes.md): Notes on a select few important policy measures covering energy efficiency, planning, and incentives in some European countries and EU directives

- [Regulation Encoding](https://github.com/Dhruv-baner/capstone_edf_2026/blob/main/regulation_encoding.ipynb): The label encoding method we applied, based on our assessment of the provisions of policies from across various countries. We scored each country on how stringent energy efficiency, sustainability, and zoning constraints were, as well as the incentives.

---

### **Executive Summary**

Data centres are an increasingly critical part of the global economy. They play an essential
role in powering Artificial Intelligence (AI) models, storing vast amounts of data, and providing solutions related to cloud computing. At the same time, they place an intensive demand
on resources such as energy, water, and land. To match this demand, utilities often expand or
modify the electricity grid, which can be an expensive process. The additional costs incurred
in establishing such infrastructure are often offset by households and other customers who
may not directly reap the benefits of these upgrades. Furthermore, data centre presence has
been found to drive up local electricity prices for all consumers. This leads us to the question
of fairness in the cost allocation of energy and infrastructure to support data centres, and
whether it is fair for households to be bearing the brunt of the steep costs associated with
powering data centre infrastructure. To address this, many countries have developed regulatory frameworks meant to mitigate the potentially harmful effects of such infrastructure.

The objective of this report is to study how the growing presence of data centres relates to
a range of variables, including electricity price, international energy trade, energy generation
mix (fossil, renewable, nuclear), geographical factors (population, land area), and different
categories of regulatory frameworks (planning, reporting, sustainability, and incentives). The
research problem is multi-faceted, involving several factors that are possibly intertwined. The
complexity of these relationships makes it important to distinguish correlation and causality,
as seemingly meaningful relationships could be spurious or directionally complicated. Furthermore, countries do not exist in a vacuum; their relationships with each other (such as
how they trade electricity) are important to consider.

In order to uncover these relationships, we adopted a four-part methodology, which all
come together to provide a holistic view of our research problem. The first part is based on a
careful study of regulatory frameworks implemented by different countries and organisations
(such as the European Union) that were directed at data centres or similar infrastructure.
Based on this, four broad categories of regulations were identified: energy reporting, sustainability, zoning restrictions (i.e. planning), and incentives. The regulations, policies,
directives, and binding frameworks related to these categories were sourced and studied for
45 European and Eurasian countries. A criterion was developed to ordinally score each of
these countries on the different policy categories, on a scale of 0 to 3. They were then accordingly hand-coded using a label encoding process. This formed a key component of the data
for the subsequent models. We endeavoured to keep the criteria objective and measurable,
but since some decisions required discretion, we note a construct-validity limitation.

The second part of our methodology section comprises the exploratory analysis of data
from all 51 US states. We used regression analysis to test the relationship between data
centre presence and state-level energy prices. As our two key variables of interest, we felt it
was important to begin with this step, testing their effect on one another. The US context
was provides a greater sample size (n = 51 as opposed to our 29 European countries studied
later), so serves as a more statistically reliable context to analyse the relationship between
price and data centres. We do, however, acknowledge that results throughout this report,
given our two separate geographical contexts and the apparent importance of physical and
jurisdiction-specific factors in our research question, may be location-specific, and so are interpreted with this in mind.

The third part of our methodology involves the implementation of graph modelling and
network analysis. We built graph objects in R which represent electricity trade (the edges)
among 29 European countries from 2023 to 2025. Each country (node) is attached to a set
of common attributes including data centre count and energy prices, alongside our other
relevant variables, and analysed these in a pipeline of three separate techniques.
Firstly, Exponential Random Graph Modeling (ERGM) was employed to assess the relationship of our key variables with the presence of a trade tie between countries. ERGMs
estimate which structural and nodal features are associated with tie presence (the outcome
variable) in the observed network, but since our graphs are single-year, static snapshots, these
associations cannot establish a causal direction. In our case, we believe that reverse-causality
(network structure influencing data centre presence and price, rather than the reverse) is
more likely, or at least equally plausible, since trade ties are established and embedded in
fixed infrastructure, whereas data centre presence and energy prices are comparatively variable over the same period.
This is followed by cross-sectional regressions of each year’s network separately. 

These specifications included engineered network exposure variables designed to encode the structural features of the networks that emerged significant from the ERGM. This method operationalises the results of the ERGM by constructing each country’s average price gap with its
trading partners and testing its association with data centre presence via OLS regression.
The final stage of the network analysis pipeline is a Network Autocorrelation Model, which
tests whether countries’ variables move in correlation once network dependence is modelled
formally, rather than approximated by an exposure variable. The results of these methods
come together to provide an overview of the effects observed when our observations (countries) are modelled as relationally dependent (each country’s outcomes linked to its trading
partners’, not just serially correlated over time) on one another. Results are interpretated
cautiously, given relatively small (n = 29) sample size.

The fourth methodological approach in this report revolves around causal analysis. A
modern inference framework called DoWhy charted out a pipeline for causal inference, consisting of four steps: Model, Identify, Estimate, and Refute. Using the Linear Non-Gaussian
Acyclic Model (LiNGAM) for causal discovery, a Directed Acyclic Graph (DAG) was built,
which provided the basis for causal understanding. Following this, the Average Treatment
Effect (ATE) of features such as regulatory strength were tested on data centre presence
using the Backdoor Estimation Criterion, with additional tests to ensure the estimates were
trustworthy. These causal effects were used to inform a cross-sectional regression model, built
using the causally significant features.

The main practical implication of our analyses as a whole is that policy design appears
to matter for data centre growth, particularly planning frameworks and incentive schemes,
which emerge as the clearest causal levers. Network exposure regressions found incentives
regulation to be a consistently significant factor with a positive effect on data centre presence (p = 0.003 − 0.018). The most extreme effect is driven solely by Ireland; however,
but our small sample size means this does not invalidate the finding, but rather warrants
further research. Cross-sectional causal-aware regressions all confirmed the positive significant effect of incentives regulation. Planning regulation appears significant (p = 0.037) in its
DoWhy causal estimand, similarly exhibiting a positive effect on the presence of data centres.
Causal analysis identifies sustainability regulation as relevant, though this is more indirect,
intertwined with broader institutional context. These findings are directly relevant to policymakers seeking to attract data centre investment or manage its spatial and infrastructural
consequences.

The ERGM shows a link between data centre presence and energy trade ties and a highly
significant relationship between trade and price differences between countries. The Network
Autocorrelation model confirms that countries’ prices are not independent of one another
(LR = 12.9 − 21.6, p < 0.001), whilst US data linear regressions showed that price is a
significant predictor of data centres (p = 0.011 − 0.012−). Although the coefficient sign flips
upon controlling for population via a per-capita data centre measure, the significance of this
relationship is the key insight here. Holistically, these findings indicate that countries linked
by energy trade affect each other’s prices, which we found separately to have a relationship
with data centres; indirectly linking our key variables. The causal mechanisms involved in
this warrant further empirical study, presenting opportunity for further research.

This is not the only avenue for further research that our study opens up. Future work could
build on our causal analysis to employ double machine learning or causal forests to capture
non-linear and heterogeneous treatment effects while retaining DAG-informed adjustment
sets. On the data side, extending the panel to a longer time horizon and incorporating more
granular measures of variables would enable richer causal identification, possibly including
the use of instrumental variables based on exogenous shocks or historical policy discontinuities. Crucially, further study considering a wider global scope would aid in a better holistic
understanding of this highly complex and fast-growing problem.
