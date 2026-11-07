# GHL Funnel Ecommerce GTM Event Listener

**Free Google Tag Manager code for GoHighLevel funnel ecommerce tracking in GA4.** It sends `view_item` on your sales page, `begin_checkout` on your order page and `purchase` on your thank-you page, with the price read from the page, so you can see GHL funnel sales and revenue in GA4 and Google Ads.

![GHL Funnel Ecommerce GTM Event Listener](docs/banner.png)

**Full guide, install video and copy button:** https://mdniamul.com/gtm-event-listeners/ghl-funnel-ecommerce-gtm-listener/

---

## What it does

Edit the `FUNNEL` paths at the top of the code, then it pushes standard GA4 ecommerce events:

```js
{ event: 'view_item',      ecommerce: { currency: 'USD', value: 27, items: [...] } }
{ event: 'begin_checkout', ecommerce: { currency: 'USD', value: 27, items: [...] } }
{ event: 'purchase',       ecommerce: { currency: 'USD', value: 124, transaction_id: 'TXN-...', items: [...] } }
```

Built-in safety:

- Waits for the page to load before reading the price
- Picks the price closest to words like "today" or "total", so a crossed-out "was $97" is skipped
- Never records a $0 purchase when no total is found
- Never records the same purchase twice when the thank-you page is reloaded
- Clears the previous `ecommerce` object before each push (GA4 best practice)

## Install in 6 steps

1. **Add GTM to your funnel.** In GoHighLevel open the funnel → **Settings** → **Head tracking code** and paste your GTM container code.
2. **GTM → Tags → New → Custom HTML.** Paste [`ghl-funnel-ecommerce-gtm-listener.html`](ghl-funnel-ecommerce-gtm-listener.html). Trigger: **All Pages**.
3. **Edit `FUNNEL`** at the top: your currency and the paths of your sales, order and thank-you pages (the part after your domain).
4. **Triggers → New → Custom Event** for `view_item`, `begin_checkout` and `purchase`.
5. **GA4 Event tag** with Event name `{{Event}}` on those triggers, and tick **Send Ecommerce data → Data Layer**. Add your Google Ads purchase conversion on the `purchase` trigger.
6. **Preview**, walk through the funnel with a test order, check GA4 DebugView, then **Publish**.

## Files

| File | What it is |
|---|---|
| `ghl-funnel-ecommerce-gtm-listener.html` | Ready to paste into a GTM Custom HTML tag |
| `ghl-funnel-ecommerce-gtm-listener.js` | Same code without the `<script>` tags |
| `examples/sample-datalayer-output.json` | What the pushes look like |

## Videos

- Install the free code: https://mdniamul.com/gtm-event-listeners/ghl-funnel-ecommerce-gtm-listener/#install-video
- What the advanced version collects: https://mdniamul.com/gtm-event-listeners/ghl-funnel-ecommerce-gtm-listener/#advanced

## Step-by-step guides

- [GoHighLevel conversion tracking in GA4 and Google Ads](https://mdniamul.com/blog/gohighlevel-conversion-tracking-ga4-google-ads/)
- [Third-party checkout conversion tracking with Google Tag Manager](https://mdniamul.com/blog/third-party-checkout-conversion-tracking-with-google-tag-manager/)
- [Funnelish tracking setup with GA4](https://mdniamul.com/blog/funnelish-tracking-setup-ga4-triple-whale-clarity/)

## Need the full funnel? Advanced version

The free code covers three steps. The **advanced version** tracks the whole GHL funnel: `view_item`, `add_to_cart`, `lead`, `begin_checkout`, `add_payment_info` (card or PayPal), every upsell accepted, declined and paid (`oto1_offer_accepted` and so on), and one `purchase` that adds up the main offer plus every upsell taken. It also sends `user_data` for Enhanced Conversions, the buyer's SHA-256 hashed email, name and phone, UTM values, 17 ad click IDs, first-party cookies, visitor location and an `event_id` for Meta CAPI deduplication.

It comes with a setup video, a PDF guide and a GTM import file in your client portal. The code starts from $89, and setup packages are available:

- Prices: https://mdniamul.com/gtm-event-listeners/ghl-funnel-ecommerce-gtm-listener/#pricing
- WhatsApp: https://api.whatsapp.com/send?phone=8801776485758
- Book a call: https://calendly.com/mdniamul
- All listeners: https://mdniamul.com/gtm-event-listeners/

Want it done for you? See my [third-party checkout conversion tracking service](https://mdniamul.com/third-party-checkout-conversion-tracking-services/) and the [GoHighLevel conversion tracking specialist](https://mdniamul.com/gohighlevel-conversion-tracking-specialist/) page.

## Troubleshooting

- **No events:** GTM is not in the funnel's head tracking code, or the paths in `FUNNEL` do not match. Type `location.pathname` in the console on each page and copy it.
- **Wrong price:** the page shows a different price near "today". Edit the hint words in `readPrice(...)`.
- **No purchase:** the thank-you page does not show an order total. Show the total there.

## About

Built by **[MD Niamul](https://mdniamul.com)**, GoHighLevel & AI Agent Automation, Marketing Attribution and Server-Side Tracking Specialist. Founder of Digital Soldier Agency and official Stape partner.

[Website](https://mdniamul.com) · [Free GTM listeners](https://mdniamul.com/gtm-event-listeners/) · [Book a call](https://calendly.com/mdniamul) · [LinkedIn](https://linkedin.com/in/mdniamul)

## License

MIT. Free to use on your own and your clients' sites. See [LICENSE](LICENSE).
