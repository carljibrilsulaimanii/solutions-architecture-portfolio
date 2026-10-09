# Systems & Integration Architecture Portfolio

**C. Jibril Sulaiman II** · AWS Certified Solutions Architect, Associate · [jibrilsulaiman.com](https://jibrilsulaiman.com)

Original architecture work from three companies across fifteen years, organized by the problem each system solves. Every record covers the problem, the design decisions, the patterns it demonstrates, and a redrawn diagram, with the original diagrams alongside where they exist.

**View the full portfolio:** open [`index.html`](index.html), or the GitHub Pages site if enabled for this repo.

## Empify (Sept 2025 to present) · Sr. Manager, Marketing Technology & Revenue Systems

Revenue systems for a financial education company that runs weekly live free classes. Ten systems, 25 linked public repos. Built the HubSpot revenue platform from an empty portal in summer 2026 and integrated payments, community, SMS, calling and ad platforms into one data model.

| System | Patterns | Code |
|---|---|---|
| HubSpot Revenue Data Model | 9 custom objects, `class_session` join key, schema migration, first / last touch attribution |  |
| Stripe Revenue Mirror & Payment Routing | Webhook mirror, router fan-out, test vs prod isolation, $0 checkout sync | [stripe-webhooks-to-hubspot-custom-events](https://github.com/carljibrilsulaimanii/stripe-webhooks-to-hubspot-custom-events) · [hubspot-stripe-payment-product-names-and-routing](https://github.com/carljibrilsulaimanii/hubspot-stripe-payment-product-names-and-routing) · [stripe-test-mode-to-hubspot-payment-mirror](https://github.com/carljibrilsulaimanii/stripe-test-mode-to-hubspot-payment-mirror) · [hubspot-stripe-zero-dollar-checkout-sync](https://github.com/carljibrilsulaimanii/hubspot-stripe-zero-dollar-checkout-sync) |
| Conversion Attribution Pipeline | UTM cookie to checkout, server-side Meta CAPI and Google Ads conversions | [hubspot-order-form-stripe-checkout-link-integration](https://github.com/carljibrilsulaimanii/hubspot-order-form-stripe-checkout-link-integration) · [hubspot-stripe-utm-attribution](https://github.com/carljibrilsulaimanii/hubspot-stripe-utm-attribution) · [hubspot-capi-server-side-lead-and-purchase-conversions-meta-google](https://github.com/carljibrilsulaimanii/hubspot-capi-server-side-lead-and-purchase-conversions-meta-google) · [claude-meta-ads-api-access-without-mcp](https://github.com/carljibrilsulaimanii/claude-meta-ads-api-access-without-mcp) |
| Free Class Engine | Configuration object for dynamic funnels, calendar bridge, SMS campaign scheduler | [ghl-custom-values-in-hubspot-for-dynamically-updating-funnels](https://github.com/carljibrilsulaimanii/ghl-custom-values-in-hubspot-for-dynamically-updating-funnels) · [custom-add-to-calendar-bridge](https://github.com/carljibrilsulaimanii/custom-add-to-calendar-bridge) · [gohighlevel-slicktext-sms-sync-and-campaign-scheduler](https://github.com/carljibrilsulaimanii/gohighlevel-slicktext-sms-sync-and-campaign-scheduler) |
| Member Lifecycle & Retention | Community webhook router, failed-payment dunning, engagement sync, onboarding bot | [mighty-networks-webhook-router-gohighlevel](https://github.com/carljibrilsulaimanii/mighty-networks-webhook-router-gohighlevel) · [stripe-gohighlevel-failed-payment-recovery](https://github.com/carljibrilsulaimanii/stripe-gohighlevel-failed-payment-recovery) · [mighty-networks-hubspot-last-visited-sync](https://github.com/carljibrilsulaimanii/mighty-networks-hubspot-last-visited-sync) · [mighty-networks-course-progress-to-gohighlevel-custom-objects](https://github.com/carljibrilsulaimanii/mighty-networks-course-progress-to-gohighlevel-custom-objects) · [gohighlevel-conversation-ai-onboarding-activation-bot](https://github.com/carljibrilsulaimanii/gohighlevel-conversation-ai-onboarding-activation-bot) |
| Sales Routing & Conversations | AI booking, DM integration, filtered SMS inboxes | [aloware-ai-hubspot-scheduling](https://github.com/carljibrilsulaimanii/aloware-ai-hubspot-scheduling) · [mighty-networks-hubspot-dm-integration](https://github.com/carljibrilsulaimanii/mighty-networks-hubspot-dm-integration) · [filtered-sms-inboxes-auto-update-outbound-channel](https://github.com/carljibrilsulaimanii/filtered-sms-inboxes-auto-update-outbound-channel) |
| Conversational AI & Knowledge Pipeline | Bulk call transcription, speaker-labeled meeting transcripts, live-chat question export | [twilio-call-recordings-bulk-transcription-elevateai](https://github.com/carljibrilsulaimanii/twilio-call-recordings-bulk-transcription-elevateai) · [gemini-long-meeting-transcription-with-speaker-labels](https://github.com/carljibrilsulaimanii/gemini-long-meeting-transcription-with-speaker-labels) · [youtube-live-chat-questions-export](https://github.com/carljibrilsulaimanii/youtube-live-chat-questions-export) · [python-utility-scripts](https://github.com/carljibrilsulaimanii/python-utility-scripts) |
| Email Infrastructure Re-architecture | Dedicated sending domains, SPF / DKIM / DMARC / PTR, deliverability isolation |  |
| CRM Consolidation & Platform Migration | ActiveCampaign + 2 GHL accounts to GHL, then HubSpot hybrid | [activecampaign-bulk-contact-delete](https://github.com/carljibrilsulaimanii/activecampaign-bulk-contact-delete) |
| Salesforce Referral-to-Delivery (independent build, Sept 2026) | Referral intake to delivered project, record-triggered automation · [demo video](https://youtu.be/ps1hYrhsKBM) | [salesforce-referral-to-delivered-project](https://github.com/carljibrilsulaimanii/salesforce-referral-to-delivered-project) |

```mermaid
flowchart TD
  ST[Stripe webhooks] --> PM[(Payment mirror)]
  PM --> EN[Enrich: product · revenue type · class_session · UTMs]
  EN --> R{Master payment router}
  R --> T1[Tickets]
  R --> T2[Accelerator]
  R --> T3[Membership]
  EN --> CAPI[Meta CAPI, once per payment]
  AD[(Ad spend daily)] -. class_session .- PM
```

## Era 1 · Pay Cell Systems Inc. (c. 2011–2014) · President

Prepaid wireless payments platform: subscribers refill airtime by phone, text, web, app or in-store kiosk, settled through card gateways and fulfilled through airtime distributor APIs.

| System | Patterns |
|---|---|
| Cell Pay Distribution Platform | Multi-tenant SaaS, merchant-of-record design, partner API credentials, revenue share model |
| Pay-by-Phone IVR | Authorize.net, XML airtime API, async fulfillment, failure-path design, attribution |
| Self-Service Payment Kiosk | Hardware events, state machine, per-step timeouts, shared services |
| Fulfillment & Card Authentication | 3-D Secure sequence, DTMF auto-dialer (RPA on a phone line) |
| Dealer Portal Roadmap | Build vs buy, cost estimation, unit pricing |
| Feature Marketplace Sketch | Two-sided marketplace, escrow, social as event bus |

```mermaid
flowchart TD
  S[Subscriber] --> C{{Phone · Text · Web · App}}
  C --> CP[Cell Pay orchestration]
  CP -- card auth --> G[Merchant's gateway<br/>Authorize.net · Stripe · PayPal]
  G -- funds --> M[(Retailer or distributor account)]
  CP -- pull PIN --> D[Distributor airtime account]
  D --> T[Carrier / TSP]
  CP -- load airtime --> S
```

## Era 2 · Incluzion / Spendwith Corp (c. 2019–2021) · CEO / Founder, then CTO

Remote-work platform for Black and Latinx professionals: jobs board, services marketplace, learning platform and community.

| System | Patterns |
|---|---|
| ATS Translator API | Adapter pattern, canonical data model across 7 ATSs |
| Job Import Pipeline | ETL, idempotent upsert, entity resolution, lineage tags, white label |
| Incluzion Platform Map | Closed-loop CRM write-back, browser extension, observability log |
| Split Placement Network | Role-based views, feature flag on record, marketplace spec |
| Segmented GTM Funnel | ICP segmentation, tiered pricing, packaging by integration state |
| Speed-to-Lead Automation | Event-driven workflow, business-hours guard, exit conditions |
| Incluzion Operating Model | Ownership mapping, org design |

```mermaid
flowchart LR
  GH[Greenhouse] --> T
  LV[Lever] --> T
  WK[Workable] --> T
  SR[SmartRecruiters] --> T
  T{{Translator}} --> C[(Canonical job model)]
  C --> F[Job board + white-label sites]
```

## Repository contents

- `index.html` — the full portfolio page (self-contained; Mermaid diagrams render in the browser)
- `pc/` — original diagrams and whiteboard photos

Client contact details and a test phone number in two original diagrams have been left out on purpose.
