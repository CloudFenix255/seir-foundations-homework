# SEIR Foundations — Week 4 Homework
## Seven Alerts, Seven Wins

**Student:** Sid Owsley (CloudFenix255)  
**Date completed:** November 22, 2026

## Homework Questions

### HW2 — Which severities arrived, and why?
With `SLACK_ALERT_SEVERITY=INFO`, INFO, WARNING, ERROR, and CRITICAL all reached Slack. When I changed the threshold to CRITICAL, only CRITICAL was delivered. The other three severities were filtered out.

### HW3 — How many hours apart are server time and your wall clock?
My EC2 instance reports UTC and my local time in Rio de Janeiro is UTC-3, so the clocks are three hours apart. I verified 21:31:47 UTC against 18:31:47 local time.

### HW4 — Why is a quiet INFO good design, not a failure?
My disk was about 25.4% used, well below the normal WARNING threshold of 75%. An INFO confirms that the check ran successfully without making a healthy system look like an incident. This reduces alert fatigue.

### HW5 — What would make CPU load spike on the Balerica Bank?
High transaction or API traffic, heavy database queries, batch processing, or an application issue could raise CPU load. My initial check showed a load average of 0.00 on two CPUs.

### HW6 — Which fake incident deserves to wake a human at 3 AM?
I would prioritize the CRITICAL account lookup failure where the ledger file cannot be reached (code 12), because it could disrupt core banking operations. A sustained payments outage would also require immediate investigation.

## Experiments

### Experiment 1 — Severity filtering
**Prediction:** One of the four messages would arrive with `SLACK_ALERT_SEVERITY=CRITICAL`.

**Actual:** INFO, WARNING, and ERROR were skipped; CRITICAL was delivered. My prediction was correct.

### Experiment 2 — Kill switch
I set `SLACK_ALERTS_ENABLED=false` and ran `hw1_hello_slack.py`. The script skipped its alert. The kill switch is useful during planned maintenance because it prevents unnecessary notifications.

### Experiment 3 — Disk threshold
I changed the WARNING threshold from 75% to 20%. With disk utilization at 25.4%, `hw4_disk_watch.py` changed its severity from INFO to WARNING and delivered the message to Slack. I then restored the threshold to 75%.

## Final Configuration
- `SLACK_ALERTS_ENABLED=true`
- `SLACK_ALERT_SEVERITY=INFO`
- Disk WARNING threshold: 75%
- Disk ERROR threshold: 90%

## Evidence
- Slack screenshot showing alerts from at least five different homework scripts
- Terminal screenshot showing `whoami`, local time, EC2 instance ID, and `hw7_morning_report.py` output

## Result
All seven scripts ran successfully, all three experiments were completed, and the monitoring configuration was restored.
