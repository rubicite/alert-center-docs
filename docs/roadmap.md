# Roadmap

Alert Center is evolving rapidly. Here's what we're shipping—and what's coming next.

## Currently Available (v1.0)

✅ **Core Notification Engine**
- Trigger-driven architecture  
- Real-time event processing  
- Condition-based rule evaluation  

✅ **Multi-Channel Delivery**
- Email with HTML templates  
- In-app bell notifications  
- Delayed and batched delivery  

✅ **Smart Recipient Resolution**
- Explicit, hierarchical, and role-based routing  
- Relationship-based recipient lookup  
- SOQL-based dynamic resolution  
- Fallback chains and escalation  

✅ **Enterprise Governance**
- FLS and CRUD enforcement  
- Sharing model compliance  
- Audit logging (every notification tracked)  
- Rate limiting and notification control  

✅ **Configuration Framework**
- No-code rule builder for admins  
- Template editor and customization  
- Lightweight extensibility for developers  

✅ **Documentation & Support**
- Installation guide  
- Configuration playbooks  
- API documentation  
- FAQ and troubleshooting  

---

## Q1 2026: Scheduling & Batching

**Smart Time Windows**
- Send notifications only during business hours  
- Respect time zones across global teams  
- Quiet hours and blackout windows  
- User preference overrides (opt-in to urgent-only outside hours)  

**Digest & Rollup**
- Daily, weekly, or custom summary digests  
- Grouped by priority, sender, or record type  
- Reduce notification fatigue while improving visibility  
- Separate channels for urgent vs. summary  

**Delayed Execution**
- Queue notifications for specific times  
- Recurring triggers (daily standups, weekly reviews)  
- Cron-based scheduling  

---

## Q1 2026: Slack Integration

**Send Alerts to Slack**
- Real-time notifications in Slack channels  
- Direct messages to channel members  
- Interactive buttons (Approve, Snooze, View Record)  
- Threaded conversations tied to Salesforce records  

**Slack → Salesforce Feedback Loop**
- Users act on Slack notifications and update Salesforce  
- Click "View" to jump to the record in Salesforce  
- Rich previews of related records and context  

**Channel Routing**
- Route alerts to #sales, #customer-success, #finance-approvals, etc.  
- Per-user Slack DM routing for high-priority alerts  

---

## Q2 2026: Predictive Recipient Routing

**AI-Powered Routing**
- Learn which recipients historically engage with specific alert types  
- Route based on past behavior (who actually acts on alerts)  
- Eliminate notification noise by predicting engagement  

**Availability & Capacity**
- Route to available team members (based on calendar, Slack status)  
- Load-balance high-volume alerts across teams  
- Time-shift notifications based on team capacity  

**Smart Escalation**
- Automatic escalation if no one engages within X minutes  
- Escalate to manager if owner is out of office  
- Route to secondary queue if primary recipient is unreachable  

---

## Q2 2026: Webhook Extensibility

**Outbound Webhooks**
- Fire webhooks when notifications are sent  
- Integrate with your custom systems, IFTTT, Zapier  
- Trigger downstream workflows (Slack, Teams, Jira, etc.)  

**Inbound Webhooks**
- Accept data from external systems and trigger Salesforce workflows  
- Correlate external events with Salesforce records  

**Webhook Templates**
- Pre-built templates for common integrations  
- Payload customization via simple UI  
- Retry logic and error handling built-in  

---

## Q2 2026: Microsoft Teams Integration

**Send Alerts to Teams**
- Real-time notifications in Teams channels  
- Direct messages to team members  
- Adaptive Cards with rich context  
- Interactive actions (Approve, View, Snooze)  

**Teams → Salesforce**
- Click-through to Salesforce records  
- Bi-directional sync for approvals  

---

## H2 2026: Advanced Features (In Exploration)

🚀 **Custom Notification Channels**
- SMS and voice alerts  
- Push notifications to mobile apps  
- Custom HTTP endpoints  
- Integration with third-party notification services  

🚀 **Analytics & Reporting**
- Notification delivery metrics (sent, delivered, opened, acted upon)  
- Engagement analytics by rule, user, and channel  
- SLA tracking (time to alert, time to action)  
- Dashboard templates for ops, finance, and leadership  

🚀 **Workflow Automation**
- Trigger Salesforce Flows based on notification actions  
- Auto-escalation workflows based on engagement rules  
- Conditional follow-up alerts  

🚀 **Template Library**
- Pre-built notification templates by use case (sales, support, finance)  
- Industry-specific playbooks  
- Template versioning and A/B testing  

---

## How to Request Features

Have an idea? Want to vote on a feature?

1. [Create a discussion in our community](https://github.com/rubicite/Alert-Center/discussions)  
2. Vote on existing feature requests  
3. Share use cases and requirements  

Your feedback shapes our roadmap. We listen to what matters to you.

---

## Support Timeline

- **v1.0**: 12 months of active support  
- **v2.0**: TBD (estimated Q4 2026)  

---

[← Back to Home](../) | [View Features →](../features/)
