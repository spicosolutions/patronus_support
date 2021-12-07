# Patronus
![alt text](https://i.imgur.com/apT3WtE.jpg)


## Introduction
### About

Patronus provides security teams the ability to easily monitor, detect, and react to security concerns based on a scoring system that highlights notables and filters out the noise. Spend less time searching and more time logically drilling down to determine how events correlate to form a story.

Too often we see customers struggling with these challenges:
- SOC teams spending hours focused on clearing noise instead of focusing on real problems
- Bouncing from view to view trying to isolate events that caused problems
- Struggling to build a timeline of events to determine if an issue is real or a false positive
- Correlation that is less about correlating different triggering events and more about identifying something that might be considered "notable"

The Patronus SIEM provides security teams the ability to easily monitor, detect and react to security concerns based on a scoring system that highlights notables and filters out the noise. Spend less time searching and more time logically drilling down to determine how events correlate to form a story.

A basic scoring system was put in place which applies a certain level of risk to ALL detections. Those detections become compelling as they grow in score and then generate an incident after a prescribed threshold is exceeded.

We believe that many events generate an incident and a timeline vs every incident representing a single event. This greatly reduces the time spent in lifecycle management and chasing false positives.

Quite simply, time is the asset that is most important to a security team.
- Time to detection
- Time to investigation
- Time to remediate

### Key Features
Executive View
- Summary of security posture
- High level details of incidents, risks and threats identified

Score based incident generation
- Noise reduction
- Engine that focuses on Cross-layer risk generation which makes for a more reliable incident.
- The score of the many is better than the score of one

Incident Management
- Organized operations for your SOC
- Immutable note taking for incident reporting

Threat Hunting Scoreboard
- The Patronus Scoreboard provides a single real-time view of risk generating activities
- Timeline view for risk objects as well as risk generating events
- Drilldown to the records generating risk all in a single view
- Watch list for risk generating objects

Threat Management
- System which ingests available threat feeds for ips, domains and files
- Canned queries to match events to IOCs

### Release Notes

## Planning
### Requirements
- Splunk Enterprise or Splunk Cloud >v8
- If Splunk Cloud, turn off "App jailing" via suport
- Splunkbase applications

| Application                     | Version |
| ------------------------------- | -------- |
| ES Content Updates | 3.0.4 |
| Splunk Security Essentials | 3.1.2 |
| Event Timeline Viz | 1.5.0 |
| Lookup Editor | 3.4.6 |
| JSON Tools | 0.2.0 |
| Missile Map | 1.2.3 |
| Splunk Common Information Model | 4.19.0 |
| Number Display Viz | 1.6.8 |

## Installation
### Splunk Enterprise
### Splunk Cloud

## Upgrades

## Using Patronus
