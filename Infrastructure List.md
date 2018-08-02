## Security
### Must Have
* Threat model for the system	
* HTTPS Everywhere, by default, with automated cert renewal	
* Authn/authz model that is threat modeled and secure	
* Proper IAM access controls	
* SSH Keys, System User Accounts
* Jumphost, VPN	
* Proper networking (on CMSNet?)	
* Sub 5 minute deploys for hotfixe
* Proper storage of credentials (for third party systems) 	
* Backup/protection of any other sensitive data	

### Nice To Have
* Internal Package Mirror (Already done by AWS?)	
* Sub 30s deploys for hotfixes	


## Stability
### Must Have
* Threat model for system stability	
* Alerting (Pagerduty) 	
* Monitoring (CloudWatch, New Relic) 	
* Log collection (Splunk) 	
* Safe deployment process for infrastructure	
* Safe deployment scripts for code (immutable, canaries, rollbacks)	
* No single points of failure	
* Basic periodic pings for uptime monitoring	
* Outage/disaster recovery tests	

### Nice To Have
* Automatic rollbacks	
* Automatic recovery of all components	

## Usability
### Must Have
* Clear architecture documentation	
* Clear usage documentation	
* Script to completely encapsulate safe code deployment 	
* Safe instance deployment	
* Safe infrastructure deployment process	
* Automated CI that runs unit tests for code	
* Clear way to set up DNS entries to point at endpoints	

### Nice To Have
* Footguns have been covered, it's hard to accidentally cause downtime
* Automated CI for terraform modules
* Automated CI for AMI builds
* Push button deploys
* Continuous deployment in lower environments