# One hosted provider for feed, email, and browser push

Research for [Which single provider delivers the feed, email and web push?](https://github.com/Bearded-Productions/ai_hero_training/issues/25), checked 2026-11-18. This is research, not a vendor selection or signup. Only public primary sources were used; no delivery or account-entitlement test was performed.

**Result: no fully verified current match.** NotificationAPI/Pingram is the strongest conditional candidate: its published technical material covers the requested architecture, including managed production email. However, current public pages do not establish that new accounts receive the headless inbox, browser push, and enforced user authentication on a usable free development tier. Engagespot's default-email quick start does not establish production delivery entitlement.

The hard requirements are one hosted account, headless per-user feed, email, browser web push, secure feed authentication, backend triggers, and a usable free development tier. Production may be paid. Vendor-managed upstream infrastructure is acceptable; customer-provisioned SendGrid, SES, Firebase, etc. accounts are not. Category/channel preferences are desirable, not mandatory. DNS verification and a website service worker are setup work, not extra delivery accounts.

## Strongest conditional candidate: NotificationAPI / Pingram

NotificationAPI's [pricing URL](https://www.notificationapi.com/pricing) and [documentation root](https://docs.notificationapi.com/) now redirect to Pingram. Separate older NotificationAPI documentation and indexed pages remain available, so their historical capabilities must not automatically be treated as current new-account entitlements.

| Requirement | Evidence and assessment |
| --- | --- |
| Production email without another delivery account | **Verified in current docs.** Pingram says it handles SMTP and delivery infrastructure, explicitly removing the need for SendGrid, SES, or Mailgun. Development can use its own sender domain; production requires/recommends DNS verification of the customer's domain. This is managed delivery, not merely a test-email service. [Email overview](https://www.pingram.io/docs/email/overview) |
| Free development allowance | Current pricing advertises up to **3,000 emails/month**, no credit card. It does **not** list inbox or browser-push allowances or Secure Mode entitlement. Do not infer those channels are included from free email. The page inconsistently describes mixed SMS/email/voice allowances as “or” versus “and”; email-only allowance is sufficient for this comparison. [Pricing](https://www.pingram.io/pricing) |
| Browser push without Firebase account | The indexed Pingram guide documents SDK-managed subscriptions/VAPID keys, a service worker, permission, and backend sends; its setup requires a Pingram account, not a Firebase project. Direct retrieval returned 403 during this investigation, so this is indexed official evidence with a freshness/access limitation. [Web-push guide](https://www.pingram.io/docs/channels/web-push) |
| Headless feed operations | Older official React documentation exposes notification objects and preferences through context, plus functions to update state, and describes websocket updates. It supports a custom UI rather than requiring the packaged inbox. However, opening the old SDK URL now redirects to a Pingram page that redirects to the docs root. Current new-account availability, pagination/retention limits, and supported SDK contract remain unverified. [Older React SDK source/index](https://docs.notificationapi.com/reference/react-sdk), [current redirect target](https://www.pingram.io/docs/reference/react-sdk) |
| Secure per-user feed access | Older official Secure Mode docs describe server-generated keyed user-ID hashes and rejection of requests lacking a valid hash after Secure Mode is enabled. Thus plain client-side `userId` is insufficient. The current Pingram Secure Mode URL redirects to a general security page, leaving new-account enablement and plan entitlement unclear. [Legacy Secure Mode](https://www.notificationapi.com/docs/security/secure-mode/), [current redirect](https://www.pingram.io/docs/security/secure-mode), [current security page](https://www.pingram.io/docs/security/security-at-notificationapi) |
| Backend trigger | Current `POST /send` reference includes `EMAIL`, `INAPP_WEB`, and `WEB_PUSH`, recipient identity, and inline feed/push payloads. This supports technical plausibility, but API schema fields alone do not prove channel entitlement. [Send API](https://www.pingram.io/docs/api-reference/operations/send/) |
| Vendor-stored preferences | Older React context includes preferences, and Secure Mode protects preference reads/writes. Current category/channel preference availability is unverified. Optional requirement, so not independently disqualifying. [React SDK](https://docs.notificationapi.com/reference/react-sdk), [Secure Mode](https://www.notificationapi.com/docs/security/secure-mode/) |

**Interpretation:** this is not evidence that Pingram discontinued these features. Current pricing/docs emphasize email, SMS, and voice while older inbox/push integration pages redirect or are inaccessible. It is an unresolved product/entitlement gap, not a confirmed incompatibility. [Current docs index](https://www.pingram.io/docs/), [current pricing](https://www.pingram.io/pricing).

## Engagespot: default email is not proof of production delivery

The [quick start](https://docs.engagespot.co/docs/introduction/quick-start/) says default email and SMS providers are enabled. But [channel setup](https://docs.engagespot.co/docs/features/channels/concepts/enabling-a-channel/) says only in-app is enabled by default and customers must sign up for third-party providers themselves. These official pages conflict; neither establishes the default email service's limits, sender verification, or production entitlement.

Engagespot has a [default web-push provider](https://docs.engagespot.co/docs/features/channels/web-push/default-web-push-provider/), so browser delivery is a promising part of its offering. Its [environment guide](https://docs.engagespot.co/docs/concepts/environment/) documents development and production environments, but an environment named “production” does not prove bundled production email. The [pricing page](https://engagespot.co/pricing) returned 404 through the web tool; current free allowances were not independently verified from a usable first-party pricing page. **Do not classify the default email as either production-capable or definitely sandbox-only without further evidence.**

## Other alternatives checked

| Provider | Why it is not a verified match |
| --- | --- |
| Courier | Its built-in test email delivers only to the signup address; reaching real customers requires connecting a provider. A developer sandbox is not managed production email. [Official setup explanation](https://www.courier.com/guides/send-notifications-from-ai-agents) |
| Novu | Its official integration catalog routes email through customer provider accounts and push through external services. A unified API does not remove those accounts. [Channel integrations](https://www.novu.co/integrations/channels/) |
| Notibase | Explicitly requires the customer's mail server and SMS gateway. [Official quick start](https://notibase.dev/) |
| OneSignal | Its official in-app product describes mobile interstitials/carousels, not the required persistent headless web feed. No matching feed was verified in this bounded investigation. [In-app product](https://onesignal.com/in-app) |
| Customer.io | Its new web-push docs explicitly avoid Apple/Firebase accounts, making it plausible for managed delivery. But documented free access is a 14-day trial or a conditional startup program, not a verified generally usable free development tier; headless feed/auth fit was not established. [Web push](https://docs.customer.io/messaging/channels/push/web/overview/), [trial limits](https://docs.customer.io/accounts-and-workspaces/plan-features/), [pricing/startup program](https://customer.io/pricing) |

## Precise next verification

Ask Pingram, without assuming a signup or purchase: **Can a new account use a persistent headless web inbox and browser web push on the free development tier, and continue all three channels in production with only a Pingram account and sender-domain DNS verification? Which current SDK/API supports list/pagination, unread/read/archive operations and category/channel preferences; how is mandatory per-user authentication enabled; and what are the channel quotas, retention limits, and paid-plan requirements?**

For Engagespot: **Is the automatically enabled email provider a test service or supported production delivery? Can customers verify their own sender domain and send to arbitrary recipients without creating any external email-provider account, and on which plans/quotas?**

Until one vendor answers those gaps with current documentation or verified entitlement, the single-provider constraint remains unresolved. No requirements were relaxed, and no delivery accounts were created.
