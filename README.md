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

## Setup
### Configuration Management
#### Asset Management
Assets refer to the system in which Patronus is responsible for protecting.  The source(s) of asset data may come from many sourcing including Active Directory, Qualys, Tenable, JAMF, etc.  These sources are then merged into a single working copy with evaluation of each data element giving priority to data values from the more severe to less. 

This form allows for the definition of where to find the asset data that was created and stored in a lookup table.  Recommendation would be to create a Saved Search that incrementally creates the lookup table using the fields as defined below.  Please make sure that the lookup table has permissions set to Global.

Fields used to create the asset list are defined below.

| Field | Description |
| ----- | ----------- |
| key | syst em used multivalue field specifying all values that may be used for identification of an asset.  This does nit get created in the user defined lookup |
| ip | ip address |
| dns | domain name of a system as would be defined in dns. This field may also be used for defining fqdn |
| mac | unique mac address of a system |
| owner | user which owns the system |
| priority | low, medium, high, critical |
| category | a logical category for representing the purpose or use of a system |

File names MUST be in the format of patronus_asset_SYSTEM.csv

#### Identity Management
Identities refer to the users in which Patronus is responsible for protecting.  The source(s) of identity data may come from many sourcing such as Active Directory or Okta.  These sources are then merged into a single working copy with evaluation of each data element giving priority to data values from the more severe to less. 

This form allows for the definition of where to find the asset data that was created and stored in a lookup table.  Recommendation would be to create a Saved Search that incrementally creates the lookup table using the fields as defined below.  Please make sure that the lookup table has permissions set to Global.

Fields used to create the asset list are defined below.
| Field | Description |
| ----- | ----------- |
| key | system used multivalue field specifying all values that may be used for identification of a user.  This does not get created in the user defined lookup |
| user | user name |
| email | email address of the user |
| first_name | first name of the user |
| last_name | last name of the user |
| phone | phone number of the user |
| manager | direct manager of the user |
| start_date | employment start date |
| end_date | employment end date |
| priority | low, medium, high, critical |
| category | a logical category for representing the purpose or use of a system |

File names MUST be in the format of patronus_identity_SYSTEM.csv

#### Threat Feed Downloads
There are three different types of threat feeds supported by Patronus: ip, domain, file
| Type | Description |
| ----- | ----------- |
| ip threat feed | IP addresses found to be compromised or suspect.  Supported fields include: ip |
| domain threat feed | Unsafe or compromised domain names accessed via web or network.  Supported fields include: domain |
| file threat feed | Unsafe or compromised files identified by name or hash via endpoint or equivalent data feeds.  Supported fields include: file_name, file_hash |

When adding a new threat feed it is important to understand the data you are inserting:
| Field | Description |
| ----- | ----------- |
| name  | Logical name representing the threat feed |
| type  | ip, domain, file |
| url  | URL in which the threat feed can be downloaded |
| file_name  | file name to save the downloaded feed as.  Use the .csv extension |
| regex  | Regular expression to parse the data and to define the fields necessary for the typ of feed.  Depending on feed use $1 and $2 to correspond with the headers defined |
| headers  | define the headers/values represented in the threat feed |

#### Corporate Subnets
Corporate Subnet configuration refers to the location of IP CIDR ranges in your organization to allow Patronus to better understand threats.

| Field | Description |
| ----- | ----------- |
| label | textual representation of the CIDR range |
| ip/cidr | CIDR range |
| latitude | he angular distance of a place north or south of the earth's equator, or of a celestial object north or south of the celestial equator, usually expressed in degrees and minutes |
| longitude | the angular distance of a place east or west of the meridian at Greenwich, England, or west of the standard meridian of a celestial object, usually expressed in degrees and minutes. |

### Setup Check
### Validation
- Threat Management
  - All URLs must be HTTPS
  - Processed data will be visible in ss_threat
  - If no data is visible, review cim_modactions for failures related to processing due to URL issues or regex
- Asset visibility
  - Processed data will be visible in ss_asset
  - Dashboard visibility in Reference>Assets
- Identity visibility
  - Processed data will be visible in ss_identity
  - Dashboard visibility in Reference>Identities
- Users
  - Users are visible in dropdowns on Incident Management for assignment
  - Users update once an hour or can be triggerred by running 'Patronus User - Lookup Gen'

## Using Patronus
### How Scoring Works
- Risk Generation (SSIG)
Patronus is built on the concept of using scores to assess the risk in an enviornment. Correlation searches are used to identify issues and assign scores to objects that are considered risky. Each search has a base score and reliability associated with it.  Reliability helps reduce the score for searches that are noisy or unreliable. For each hit the search gets, a score based on the base score of the search and its reliability gets added to the risk object that triggered it. 

- Incident Generation (SSRG)
As scores accumulate and exceed 100 (default) an incident is generated.  An incident is a cross-layer view if risk generations against an object.  Instead of seeing each individual score generated and then having to review it, they are bubbled up to a sumamrized view and then presented to the analyst as a picture of activitues for a risk object.  This allows a story to be told instead of a single page.

### Filter Management

### Creating Risk Generators

### Incident Management

### Scoreboard
