# Key Features

## Trigger-Driven Architecture

Alert Center is built on a trigger-first model. Every event in Salesforce can become a notification.

**How it works:**
1. A record changes (opportunity, case, lead—anything)
2. Your rule evaluates the change
3. Conditions are assessed in milliseconds
4. Recipients are resolved dynamically
5. Notifications are delivered via your configured channels
6. Every step is logged and auditable

**Examples:**
- **Deal alert**: When an opportunity moves to Negotiation stage, notify the VP of Sales and the deal owner's manager
- **Case escalation**: When a case priority hits Critical and no one owns it, alert the on-call support lead
- **Forecast reminder**: Daily summary of pipeline changes, routed to each rep's email
- **Compliance flag**: When a record violates a policy rule, notify Legal—zero delivery latency

---

## Smart Condition Engine

Build complex logic without code.

- **Simple rules**: Field value equals X? Send notification
- **Complex expressions**: If opportunity amount > $50K AND stage changed AND close date < 30 days, then escalate
- **Time-based triggers**: Every morning, every Friday, on delay windows
- **Aggregate triggers**: When total pipeline in a region drops below threshold
- **Cross-object logic**: Reference related accounts, contacts, opportunities in a single rule

**Built-in functions:**
- Date math (days until close, age of record)  
- Numeric aggregation (sum, count, max, min)  
- Text matching and regex  
- Relative role and hierarchy lookups (owner's manager, account executive for region)  

---

## Recipient Resolution

Never hard-code email lists. Let Alert Center resolve them dynamically.

**Resolution modes:**
- **Explicit**: Alert the record owner
- **Hierarchical**: Owner → Manager → Director (stop at first match)
- **Role-based**: Find all Sales Reps in EMEA
- **Criteria-based**: Any user with permission_set = "Alert Admin"
- **Relationship**: The primary contact's email on the related account
- **Query-based**: Run a SOQL snippet and alert all matching users
- **Fallback chains**: Try to alert the opportunity owner; if they're inactive, alert their manager; if that fails, alert queue X

Every recipient resolution respects:
- User availability (inactive users skipped)
- FLS and CRUD (users without read access don't receive alerts)
- Sharing model (if a user can't see the record, they won't get a notification about it)

---

## Multi-Channel Delivery

### Email
- Professional HTML templates
- Personalized merge fields (recipient name, record details, hyperlinks)
- Scheduled send (immediate or batched)
- Attachments (optional)
- Reply-to governance

### In-App Bell
- Real-time notifications in Salesforce UI
- Persistent log in the notification center
- Click-through to the related record
- Dismiss or snooze
- Filter by type and date

### Delayed Delivery
- Queue critical notifications for off-hours
- Batch daily summaries
- Time-window scheduling (9am–5pm only, weekdays only, etc.)
- Respect time zones across multiple regions

---

## Enterprise Governance

### Field-Level Security (FLS)
Sensitive fields are automatically masked or excluded from notifications. If a recipient doesn't have read access to a field, it doesn't appear in their alert.

### Sharing Model Compliance
A user receives a notification only if they can access the underlying record under your org's sharing rules. No data leakage.

### CRUD Enforcement
If a user lacks read access to the object, they're skipped from the recipient list.

### Audit Trail
Every notification is logged with:
- Timestamp and trigger rule
- All recipients (attempted and delivered)
- Delivery channel and status
- Any errors or FLS redactions applied
- Full record context at time of send

### Admin Controls
- Rate limiting (max X notifications per user per day)
- Disable/enable rules without deletion
- Bulk notification retry
- Notification suppression windows
- Org-wide notification pause

---

## Configuration & Extensibility

### For Admins: No-Code Rule Builder
- Drag-and-drop condition builder
- Template editor for email body
- Recipient resolver UI
- Test mode with sample records
- Activation and scheduling controls

### For Developers: Lightweight Framework
- `AlertCenter_Condition` interface for custom logic
- `AlertCenter_Recipient` for advanced resolution
- `AlertCenter_Template` for dynamic formatting
- Full async execution (no blocking user transactions)
- Dependency injection for testability

**Example: Custom Condition**
```java
public class HighValueOpportunityCondition implements AlertCenter_Condition {
  public Boolean evaluate(SObject record) {
    Opportunity opp = (Opportunity) record;
    return opp.Amount > 100000 && opp.StageName == 'Proposal';
  }
}
```

---

## Security & Compliance

✅ **SFDC native**: Runs on platform, no external data transfer  
✅ **FLS & CRUD compliant**: Automatic redaction  
✅ **Audit logging**: Complete notification history  
✅ **Encryption**: In transit (TLS) and at rest (SFDC encryption)  
✅ **Scalable**: Built on Apex async patterns  
✅ **Governor limits aware**: Respects batch and async limits  

---

## What You Get

📦 Managed Package (AppExchange)
- Pre-built core objects and triggers
- Admin console and rule builder
- Template and recipient management
- Notification log and audit views
- Configuration examples and playbooks

📚 Complete Documentation
- Installation and setup guides
- Trigger-wiring reference
- Configuration playbooks by use case
- Extensibility framework with code samples
- Troubleshooting and FAQs

🤝 Support & Community
- Knowledge base and FAQs
- Installation support
- Standard Salesforce support channels

---

## Next: [Explore Use Cases](../usecases/)
