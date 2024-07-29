## Disclaimer 

This repository is a fork originally created from [vitobotta](https://github.com/vitobotta/velero-notifications). Later [wout-o](https://github.com/wout-o/velero-notifications) added feature for discord webhooks.

# velero-notifications

This is a simple Kubernetes controller written in Crystal that sends Email/Slack/Discord/webhook notifications when backups are performed by [Velero](https://velero.io/) in a [Kubernetes](https://kubernetes.io/) cluster.

![Screenshot](slack.png?raw=true "Screenshot")

![Screenshot](discord.png?raw=true "Screenshot")


## Installation

1. Clone the repo
2. Install with Helm 

Don't forget to change namespace && velero_namespace to your values.

```bash
helm upgrade --install \
  --namespace velero \
  --set velero_namespace=velero \
  --set notification_prefix="[Velero]" \
  --set slack.enabled=true \
  --set slack.failures_only=false \
  --set slack.webhook=https://... \
  --set slack.channel=velero \
  --set slack.username=Velero \
  --set discord.enabled=true \
  --set discord.failures_only=false \
  --set discord.webhook=https://... \
  --set discord.mentions.enabled=false \
  --set discord.mentions.failures_only=true \
  --set discord.mentions.role_id="1234567890" \
  --set email.enabled=true \
  --set email.failures_only=true \
  --set email.smtp.host=... \
  --set email.smtp.port=587 \
  --set email.smtp.username=... \
  --set email.smtp.password=... \
  --set email.from_address=... \
  --set email.to_address=... \
  --set webhook.enabled=true \
  --set webhook.failures_only=false \
  --set webhook.url=https://... \
  velero-backup-notification ./helm
```

That's it! You should now receive notifications when a backup is completed or fails. It couldn't be simpler than that!


## Quick guide on how to integrate with
* webhook (azure logic app, [healthchecks.io)](https://healthchecks.io/))
* discord webhook
...

## License

[MIT License](https://github.com/vitobotta/velero-notifications/blob/main/LICENSE)

