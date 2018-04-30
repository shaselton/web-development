# Things that need to be covered when starting a new project
## Environments
### Local/Development
### Dev
### Staging
### Production

## Feature Flags
* Redis with simple, custom backend
* [launch darkly](https://launchdarkly.com/) I've never used this, but looks decent.

## Deployment Cadence
## Testing Methodology
* TDD for both the application and server

## Testing Cadence Per Environment
### Local/Development
### Dev
### Staging
### Production
## Deployment Fixes
Roll forwards vs rollbackl (hint: if the deployment cadence is followed and optimized, a roll forward strategy should be used first)
## Security
* lots of shit to add here.
* [AWS](https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)

## Deployment Process
When changing the production environment, a certain level of communication needs to be had to:
1. notify appropriate stakeholders that cross product, opts, comms, etc.
1. ensure we're coordinating across teams (having simultaneous deployments in flight is prone to confusion)
1. have a cross-team historical record of when changes were made to easy in debugging and analysis.

We should never be making "quick" deployments (outside of emergencies) that only one or two people know about. **Deployments should be performed during normal business hours with no downtime.** When deploying new code to production the following series of events and notifications need to take place (NOTE: there is a strong preference for automated notifications using scripts):
* notify the deployment chat room (make sure you have one of these) (ideally including a link to relevant splunk/new relic dashboards for the deployment) when:
	* the deployment is starting
	* when the deployment is finished
	* if the deployment fails and why
	* if any feature flags are either introduced or changed.
* [Generate a NewRelic Deploy event:](https://docs.newrelic.com/docs/apm/new-relic-apm/maintenance/recording-deployments)
* Send out an email to our deployment distribution list – this should be a smaller set of stakeholders that are concerned with day-to-day
code changes. This email should include:
	* release notes
	* JIRA ticket numbers for the code associated with the deployment.
small, factual explanation on the deployment. e.g. "6/20 deployment included fixes to x,y,z. Feature flag
IS_FEATURE_AVAILABLE? was added and set to false to allow for a dark deployment"
	* version/tag of the branch being deployed.
* QA should run a smoke test after a successful deployment to production to ensure the environment matches Staging.
* Dev teams are expected to be available until after the smoke test has completed.

When we do need to have a quick deployment, they usually take the place [hotfixes](https://gist.github.com/wildlyinaccurate/daec7910958330a64754). Some of the reasons for having a hotfix could include identifying major bugs in the system or compliance issues such as logging PII. Deploying a hotfix follows the same steps (outside of the normal
development workflow) as a typical deployment.

## Release Process
When releasing a new feature to the public, there are typically a set of steps that are followed both on the engineering and "front office" (comms
usually) fronts. From the engineering perspective, "releasing" involves turning a set of feature flags. At the moment, feature flags are loaded via
config files thus this requires the services/project to be restarted for the config file to be reloaded. Thus:
* Release/deployment manager notifies the chat rooms when
	* A flag has changed. This should be happening in all environments, not just production.
	* When a service restart is started.
	* When a service restart is finished.
* An email to internal stakeholders that contains a curated set of release notes associated with the release.

##  Incident Response