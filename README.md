# RansomSim

A digital twin of a ransomware incident for an enterprise network. Test security and governance decisions, watch the business impact, and connect the model to external systems.

**Live demo:** https://mfmk00.github.io/ransomsim/

Built by Mohammad Alkhaldi, Senior Cyber Security Engineer.

## What it does

RansomSim models how ransomware spreads across a 12-node network (email gateway, firewall, Active Directory, workstations, servers and backups). You choose a scenario, set your defences, then make response decisions while the attack unfolds. The model shows how each decision changes infection, data theft, cost and reputation.

## Scenarios

| Scenario | What to learn |
|---|---|
| Phishing to ransomware | Lateral movement through Active Directory |
| Compromised vendor VPN | Fast spread with a short dwell time |
| Double extortion | Data theft first, regulatory exposure |
| Backup-targeted attack | What happens when backups are compromised |

## Variables you control

- EDR coverage
- Network segmentation
- SOC analysts on shift
- Age of the last backup
- Immutable or offline backups
- Simulation speed

## Decisions you can test

Isolate infected hosts, reset AD credentials, block egress and C2, run an XSOAR containment playbook, hire an IR retainer, restore from backup, notify the regulator, and pay the ransom.

## Indicators

Hour, detection status, infected and encrypted nodes, isolated nodes, data stolen (GB), cumulative cost, reputation, ransom demand, a threat badge, an impact chart and an event log. At the end of a run the model produces a decision report with a cost breakdown and governance recommendations.

## Digital twin connection

**Input (data into the twin)**
- Import a CSV or JSON file of events.
- Inject a single SIEM event from the page.
- Poll a live JSON feed URL every 5 seconds.

**Output (commands out of the twin)**
- Every decision is sent as a POST request to a webhook URL you provide, for example a SOAR playbook endpoint. It can be tested with https://webhook.site.

Example command payload:

```json
{"action":"Block egress and C2","target":"all","hour":5,"scenario":"dbl","cost_k":3}
```

## Data formats

Import events as CSV:

```
t,node,event
3,fin,infected
6,ad,infected
10,file,encrypted
11,,detect
```

Valid nodes: `fw, mail, web, ad, hr, fin, ops, it, file, erp, db, bak`
Valid events: `infected, encrypted, detect, isolate, clean`

A JSON import can also set the scenario and defences:

```json
{"scenario":"phish","edr":50,"seg":40,"an":3,"backupAge":12,"immutable":true,"events":[{"t":3,"node":"fin","event":"infected"}]}
```

Export a timeline as CSV and a full report as JSON from the Data panel.

## How to use

1. Choose a scenario.
2. Set your defences with the sliders.
3. Press **Start** and watch the attack spread.
4. Make decisions, or press **Reset** and compare a run with and without them.
5. Press **End and get report** and export the results.

A light and dark mode toggle is in the header.

## Run it locally

It is one file with no dependencies. Download `index.html` and open it in a browser.

## Notes

This is a simplified teaching model with random events. Numbers are illustrative and not a prediction for any real organisation. The webhook is a demonstration endpoint; in production it would point to a SOAR platform.
