Production deployment for DS
a.k.a [Terms and Conditions] for Content Availability & Supply Distribution
________________
## Context

For a proper collaboration between ENG and DS roles within the Content Availability & Supply Distribution Team, we have compiled the following actions to guarantee safe deployments of new changes or features in Production.

## Checklist

The following checklist contains the usual tasks to be verified for every new Production deployment.

* Included and/or verified unitary tests
* Included and/or verified integration tests
* Run local or stage test using production data
* Enabled mechanism to enable or disable the new change or feature (e.g. Feature toggle)
* Published feature toggle link on the proper Slack channel (e.g. #watcher-development)
* Ran a Shadow Test in a Production environment
* Monitored the deployment using DataDog dashboards
   * [DataDog] Watcher 
   * [DataDog] [IR] Kubernetes Services Dashboard

 All of them aren’t mandatory but it is our responsibility to verified them. Use your common sense.
## Additional recommendations (Do’s and Don’t s)

* Do communicate any new deployment on the proper Slack channel (e.g. #watcher-development) and tag the green-flag.
* Do monitor the deployment of any new change (save at least 30 minutes to monitor every deployment)
* Do not deploy new changes during peak hours (12:30 - 14:00 & 19:00 - 21:00 CET)
* Do not deploy important changes before weekends or holidays.

Remember that only ENGs are in PagerDuty and we should avoid creating unnecessary issues.