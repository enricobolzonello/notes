---
up:
  - "[[Scalability is a system's ability to cope with increased load]]"
tags:
  - atomic
created: 2024-12-17 18:14
---
Use **percentiles**, not mean. For dashboards, keep a rolling window of response times in the last 10 minutes. Every minute, calculate the median and various percentiles. 

*Averaging percentiles is mathematically meaningless* since a small number of slow requests can dominate user experience while leaving the mean unaffected.

# See also 
- [[Scalability is a system's ability to cope with increased load]] — performance measurement is how you answer the scalability questions posed in the parent note 
- [[Misjudging Reliability and Causality]] — using mean instead of percentiles is exactly the statistical misjudgement described there: ignoring the distribution and building an overcoherent picture from incomplete data 
- [[Misjudging Reliability and Causality]] — using mean instead of percentiles is exactly the statistical misjudgement described there: ignoring the distribution and building an overcoherent picture from incomplete data

# References
- [[Designing Data-Intensive Applications - Martin Kleppmann]]