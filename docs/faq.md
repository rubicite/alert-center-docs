# FAQ

## General Questions

### What is Alert Center?
Alert Center is a managed package for Salesforce that automates notification delivery across email and in-app channels. It's built on trigger-driven architecture, so every change in Salesforce can trigger smart, governed notifications.

### Who should use Alert Center?
Any organization that relies on timely information flow across sales, service, finance, or operations teams. Specifically:
- **Sales teams** needing real-time deal alerts and pipeline visibility  
- **Customer success** teams managing account health and churn risk  
- **Support teams** handling critical case escalation  
- **Finance teams** automating approval workflows  
- **RevOps** maintaining pipeline accuracy and forecast reliability  

### How is Alert Center different from Salesforce Flow?
Flow is a general-purpose automation tool. Alert Center is purpose-built for notifications:
- **Simpler UX** for non-developers building notification rules  
- **Pre-built templates** for email and notification bodies  
- **Built-in governance** (FLS, CRUD, sharing model enforcement)  
- **Audit trail** of every notification sent  
- **Multi-channel delivery** (email, in-app bell, plus Slack/Teams coming Q1 2026)  
- **Smart recipient resolution** (hierarchies, fallback chains, SOQL-based lookups)  

### Does Alert Center require code?
No. Admins build rules via a drag-and-drop interface. Developers can extend with custom logic (conditions, recipient resolvers, templates), but code is optional.

### Is Alert Center secure?
Yes. Alert Center enforces:
- **FLS and CRUD** — Sensitive fields are automatically masked  
- **Sharing model** — Users only receive alerts for records they can access  
- **Audit logging** — Every notification is tracked with full context  
- **Encryption** — In-transit (TLS) and at-rest (SFDC encryption)  
- **No external data transfer** — Runs natively on Salesforce platform  

---

## Installation & Setup

### How long does installation take?
2–4 hours from AppExchange install to your first notification, including:
- Package installation (5 min)  
- Org setup and permissions (30 min)  
- Building your first 1–2 rules (90 min)  

### What permissions does my admin need?
- Manage Installed Packages  
- Manage Custom Objects  
- Manage Flows (if using flow-based extensibility)  
- API Enabled  

Standard System Administrator profile is typically sufficient.

### Does Alert Center require custom fields on my objects?
No. It works with out-of-the-box Salesforce objects. You can optionally create custom fields (e.g., Health Score, Risk Flag) to use in conditions.

### What's the impact on org limits?
Minimal. Alert Center uses async Apex (future jobs) for delivery, so:
- No blocking user transactions  
- Email limits: Standard Salesforce email limits apply  
- Governance limits: Respects batch and async limits  

See [installation guide](../docs/guides/01-installation-guide/) for detailed capacity planning.

### Can I uninstall Alert Center?
Yes. Uninstall via Setup → Installed Packages. All custom data is preserved until you delete it manually. Notification logs are preserved (read-only).

---

## Building Rules

### What can trigger a notification?
Any Salesforce object: Opportunity, Account, Case, Lead, Contact, custom objects, etc. Triggers fire on:
- Record creation  
- Record update (specific fields or any field)  
- Scheduled (daily, weekly, custom)  

### What conditions can I use?
- **Field value**: Amount > 100000  
- **Date math**: Close Date < 30 days away  
- **Text matching**: Company Name contains "Enterprise"  
- **Aggregate**: Total pipeline in region < forecast  
- **Related object**: Account industry = "Healthcare"  
- **Formulas**: Complex expressions combining multiple fields  

See [features →](../features/#smart-condition-engine) for full list.

### How do I resolve recipients?
Alert Center supports:
- **Explicit**: Alert record owner  
- **Hierarchical**: Owner → Manager → Director  
- **Role-based**: All users in "Sales Rep" role  
- **Criteria-based**: Users with permission set "Alert Admin"  
- **Relationship**: Primary contact on related account  
- **SOQL-based**: Custom query to find recipients  
- **Fallback chains**: Try A, if not found try B, then C  

### Can I test a rule before activating?
Yes. Use the test mode in the rule builder. Select a sample record and preview the notification before it goes live.

### How do I avoid notification spam?
Alert Center includes:
- **Rate limiting**: Max X notifications per user per day  
- **Suppression windows**: Disable alerts during cutoff periods  
- **Digest batching**: Combine multiple alerts into a single email  
- **Time windows**: Send only during business hours  

### Can I deactivate rules without deleting them?
Yes. Rules have an "Active" toggle. Deactivate for testing or temporary pauses.

---

## Notifications & Delivery

### How fast are notifications delivered?
Typically 10–30 seconds from trigger event to inbox or in-app bell. Email delivery depends on Salesforce email service (usually immediate).

### What if a recipient is inactive?
Inactive users are automatically skipped. If using fallback chains, escalation moves to the next recipient in the chain.

### What if a recipient lacks FLS or CRUD?
The notification is still sent, but sensitive fields are automatically masked or excluded. Audit log notes FLS redactions.

### Can I schedule notifications for later?
Yes. Rules support:
- **Immediate** — Send right away  
- **Delayed** — Queue for specific time  
- **Batched** — Combine into digest  
- **Scheduled** — Recurring (daily, weekly, etc.)  

### Can I send to distribution lists or queues?
Yes. Use recipient resolution SOQL to find members of a public group or queue, or explicitly route to a queue.

### What happens if email delivery fails?
Failed emails are logged with error details. Admins can manually retry via the notification log UI.

---

## Governance & Compliance

### Is Alert Center HIPAA compliant?
Alert Center enforces FLS and sharing, so it respects your data governance. However, HIPAA compliance depends on your Salesforce instance configuration. Consult Salesforce HIPAA documentation and your security team.

### Does Alert Center create an audit trail?
Yes. Every notification is logged with:
- Timestamp  
- Trigger rule  
- All recipients (attempted and delivered)  
- Delivery channel and status  
- FLS redactions applied  
- Record context at time of send  

Audit logs cannot be edited or deleted.

### Can I see who opened/read a notification?
Email: Tracking is available if your email client supports open tracking. In-app bell: Yes, the system tracks when users view notifications.

### How long are audit logs retained?
Logs follow your Salesforce retention policy (typically 5 years for most orgs). Contact Salesforce support for custom retention policies.

### Is there SOC 2 compliance?
Alert Center runs on Salesforce, which is SOC 2 Type II compliant. Alert Center itself follows Salesforce's compliance standards.

---

## Troubleshooting

### A rule isn't triggering.
1. Verify the rule is **Active**  
2. Check the **trigger condition** (e.g., is the field actually changing?)  
3. Verify **FLS/CRUD** on referenced fields  
4. Check the **recipient resolution** (are recipients being found?)  
5. Review **audit logs** for error messages  

See [troubleshooting guide →](../docs/guides/05-troubleshooting/).

### Recipients aren't receiving notifications.
1. Verify recipients have **active Salesforce licenses**  
2. Check **email preferences** (notifications may be disabled)  
3. Verify **FLS/CRUD** on the record  
4. Check **recipient resolution** in the rule (is it finding the right people?)  
5. Review **audit logs** for delivery status  

### Email templates aren't rendering correctly.
1. Check **merge field syntax** (should be `{!Opportunity.Amount}`)  
2. Verify the **related object** is accessible to the recipient  
3. Test with **sample data** in the rule builder  
4. Check **HTML/plain text** toggle  

### Notifications are slow.
1. Check rule **trigger frequency** (is it firing too often?)  
2. Review **recipient resolution** complexity (SOQL queries can be slow)  
3. Check **org limits** (Are you near your daily Apex limits?)  
4. Consider **batching** to reduce delivery overhead  

---

## Pricing & Support

### How much does Alert Center cost?
Check [AppExchange listing](https://appexchange.salesforce.com) for current pricing. Pricing is based on:
- Monthly notification volume  
- Number of notification rules  
- Org size  

### Do you offer a free trial?
Yes. Install from AppExchange and you get a 30-day trial on your Salesforce org.

### What support is included?
Standard Salesforce support channels:
- Knowledge base and FAQ (this site)  
- Community discussions  
- Support cases via your Salesforce org  

Premium support is available for enterprise customers.

### Can I upgrade or downgrade my plan?
Yes. Changes take effect on your next billing cycle. Contact sales for custom plans.

---

## Next Steps

- **[View Features →](../features/)** for deep-dive into capabilities  
- **[Check Use Cases →](../usecases/)** to see how teams are deploying it  
- **[View Roadmap →](../roadmap/)** to see what's coming  
- **[Install from AppExchange →](https://appexchange.salesforce.com)**  

Have a question not covered here? [Create a discussion →](https://github.com/rubicite/Alert-Center/discussions)
