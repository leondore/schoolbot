# Go ingestor on a VPS, everything else on Cloudflare

WhatsApp needs a persistent linked-device socket, so a small Go binary (whatsmeow) runs on a VPS and does nothing but forward allowlisted Messages and media to Cloudflare; it stores only its WhatsApp session and a short-lived outbox. Batching, the agent, review, Google writes, Reminders and all state live in one TypeScript Worker on Cloudflare.

## Considered Options

- **Cloudflare Containers for the ingestor.** Rejected: the whatsmeow session would need persisting outside the container's ephemeral disk, containers restart on deploys, and connecting to WhatsApp from datacenter IPs adds ban risk, all to save a few dollars a month.
- **Everything on the VPS.** Rejected: Workflows, Durable Objects and Cron give durable waits, retries and scheduling for free that we'd otherwise build and operate ourselves.
