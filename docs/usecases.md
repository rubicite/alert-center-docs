# Use Cases

## Sales Operations: Never Miss a Deal

**Scenario:**  
Your pipeline is your lifeline. A $250K opportunity moves to Negotiation, but the deal owner is in a meeting. The VP of Sales needs to know immediately. Legal needs a heads-up on the contract terms. The customer success manager needs to prepare for onboarding.

**Alert Center solution:**
- Trigger fires when Opportunity.StageName changes to "Negotiation"
- Condition checks: Amount > $100K
- Recipients resolved: Deal owner, deal owner's manager (VP Sales), CSM for account, Legal queue
- Delivery: Immediate email to all parties; in-app bell notification
- Audit: Every send logged, including FLS redactions (Legal sees redacted pricing if CRUD-restricted)

**Result:**  
No more "I didn't know this deal moved forward." No more manual Slack messages. Governance is baked in.

---

## Customer Success: Proactive Churn Prevention

**Scenario:**  
A high-value customer's health score drops below 50. This is a churn signal. Your CS team needs to know now. The account executive needs to be looped in. The renewal manager needs to prioritize follow-up.

**Alert Center solution:**
- Trigger fires on Account.Health_Score__c change
- Condition: Health_Score__c < 50 AND ARR > $50K
- Recipients: CSM for account, AE, renewal ops specialist
- Delivery: Immediate email + in-app bell
- Smart routing: If CSM is inactive, escalate to their manager
- Delayed send: Queue a digest email to leadership every Friday

**Result:**  
Proactive, not reactive. No churn surprises. Full visibility into account health across roles.

---

## Support: Critical Case Escalation

**Scenario:**  
A customer opens a Critical case. It's a P1 outage. Every minute counts. Your support team needs immediate alert. The account's AE needs context. Management needs visibility.

**Alert Center solution:**
- Trigger: When Case.Priority = "Critical" AND Case.Status = "New"
- Condition: Account.Is_Enterprise__c = true (no noise on smaller accounts)
- Recipients: 
  - On-call support lead (via role hierarchy)
  - Account AE
  - Support manager (for visibility)
- Delivery: 
  - Email + in-app bell (immediate)
  - Escalation rule: If case unresolved after 2 hours, alert leadership
- Audit: Track response time; correlate resolution time with notification delay

**Result:**  
Critical cases get treatment from day one. Escalations are automatic. SLA breaches are prevented.

---

## Revenue Operations: Pipeline Accuracy

**Scenario:**  
You run quarterly business reviews. Deal stage creep and forecast accuracy are critical. Deals without recent updates, stalled deals, and forecast misses need active management.

**Alert Center solution:**
- **Nightly trigger**: Async job evaluates all open opportunities
- **Condition logic:**
  - Deals with no activity in 14 days → Nudge the owner
  - Deals in Sales stage for 30+ days → Escalate to manager
  - Deals with close date < 30 days but stage < "Proposal" → Alert leadership
- **Recipients**: Dynamic hierarchy (owner → manager → director) based on urgency
- **Delivery**: Daily batched email digest, grouped by severity
- **Audit**: Track which deals got alerts, when owners acted, pipeline velocity

**Result:**  
Pipeline health is actively managed, not passively reported. Deals don't stall unnoticed.

---

## Compliance & Risk: Policy Enforcement

**Scenario:**  
Your company has contract-review policies. Any deal > $1M needs legal review. Any deal with a non-standard term needs approval. Violations need immediate escalation.

**Alert Center solution:**
- **Trigger**: When Deal_Governance__c changes (custom object)
- **Condition logic:**
  - If Deal.Amount > $1M AND Legal_Approval__c = false → Alert Legal
  - If Risk_Flag__c = "High" → Alert risk officer + CFO
  - If non-standard clause detected → Alert contract team + procurement
- **Recipients**: Resolved based on risk level and deal region
- **Delivery**: Immediate email with record link + in-app bell
- **Audit**: Full compliance trail—who was alerted, when, and any actions taken

**Result:**  
Policy violations are caught in flight, not in audit. Compliance is operational, not a surprise.

---

## Executive Dashboarding: Real-Time Visibility

**Scenario:**  
Your CMO wants to know the moment pipeline drops below a monthly target. Your CFO needs to see high-risk deals in real time. Your CEO wants a morning brief of yesterday's key events.

**Alert Center solution:**
- **Daily digest**: 7am email with yesterday's key events
  - Major deals closed or lost
  - High-risk accounts with activity
  - Pipeline by region vs. forecast
- **Real-time alerts**: 
  - When ARR at risk exceeds threshold → Alert CFO
  - When a key customer renews → Alert CEO
  - When pipeline by region drops 20%+ → Alert EVP sales
- **Delivery**: Mix of email and in-app notification
- **Audit**: Executives see what matters, automatically curated

**Result:**  
Leaders are informed, not overwhelmed. Noise is filtered. Critical events bubble up instantly.

---

## Marketing & Demand Gen: Lead Handoff Automation

**Scenario:**  
A lead scores hot. Your marketing automation system updated the Lead.Lead_Score__c to 90+. Sales needs to know in real time. The account executive who owns the target account needs context. The SDR needs to be ready for follow-up.

**Alert Center solution:**
- **Trigger**: Lead.Lead_Score__c changes to > 80
- **Condition logic**:
  - If score > 80 AND industry = "Financial Services" → Route to FS specialist AE
  - If existing account → Alert AE for that account + SDR
  - If new account → Route to available SDR + manager
- **Delivery**: Immediate email with lead context (industry, company size, engagement) + in-app bell
- **Template**: Dynamic, includes lead score, recent engagement, recommended next steps
- **Audit**: Track lead handoff time; correlate alert delivery with response time

**Result:**  
Hot leads convert faster. No lag between marketing qualification and sales pickup. Full handoff visibility.

---

## Finance: PO & Contract Approval Workflows

**Scenario:**  
A customer PO arrives that needs CFO approval (> $250K). It needs to be reviewed and approved within 48 hours to avoid delivery delays.

**Alert Center solution:**
- **Trigger**: When PO object's Approval_Status__c = "Pending"
- **Condition**: Amount > 250000
- **Recipients**: CFO, Finance Manager for that region
- **Delivery**: 
  - Immediate email with PO summary, direct link to approval screen
  - 24-hour reminder if not approved
  - 48-hour escalation to Controller
- **Audit**: Full approval chain logged; SLA tracked

**Result:**  
Critical approvals don't get lost. SLAs are met. Finance has visibility.

---

## Next: [View Features →](../features/) | [Check FAQ →](../faq/)
