
## Journey 

1. Understand the business problem
2. Translate business problem to a decision/mathematical model
3. Identify the required data for the decision model
4. Define the problem scope
5. Define solution methodology
6. Build a prototype and solve instances (offline)
7. Present prototype results to stakeholders
8. Discuss productionalization strategy (alignment with Engineers)
9. If feedback is provided, incorporate feedback and go back to Step 6.
10. Evaluate potential impact, feasibility, usability, and stakeholder support
11. Define productionalization and fallback strategy for the first iteration. Two major alternatives:
	1. Batch
		1. Obtain required data (Data products - Starburst? + REST APIs)
		2. Build optimization pipeline (Argo?)
		3. Expose output data in REST API, as a table or stream. 
	2. Real-time: Microservice (Glovo K8s?) 
	   It is probably parallelised by city, zone, or store.
		1. Build request manager (API, events, chron)
		2. Obtain required data (Feature store? + REST APIs)
		3. Run optimization model 
		4. Expose output data in REST API, or event. 
12. Integration with Decision system (Backend)
13. Functional testing (ad-hoc)
14. Design and launch experiment (ad-hoc)
15. Analyze experiment results (ad-hoc)
16. Based on results, evaluate alternatives, i.e. Global deployment, keep iterating, sunset.
17. Document methodology and experiment results
18. Define the next steps (including the next iteration)