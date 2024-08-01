## Disclaimer 
This repository is a fork originally created project by [andagabr](https://github.com/andragabr/velero-backup-notification). Later [vitobotta](https://github.com/vitobotta/velero-notifications) rewrite the code in Crystal. And finally [wout-o](https://github.com/wout-o/velero-notifications) added feature for discord webhooks.

# velero-notifications
This is a simple Kubernetes controller written in Crystal that sends Email/Slack/Discord/webhook notifications when backups are performed by [Velero](https://velero.io/) in a [Kubernetes](https://kubernetes.io/) cluster.

![Screenshot](slack.png?raw=true "Screenshot")

![Screenshot](discord.png?raw=true "Screenshot")

## Installation
1. Clone the repo
2. Install with Helm 

Don't forget to change namespace && velero_namespace to your values. 
#### NOTE: Velero-backup-notification namespace HAS to be same as velero namespace!! 

```bash
helm upgrade --install \
  --namespace velero \
  --set velero_namespace=velero \
  --set notification_prefix="[Velero]" \
  --set partially_failed_count_as_completed="false" \
  --set slack.enabled=true \
  --set slack.failures_only=false \
  --set slack.webhook=https://... \
  --set slack.channel=velero \
  --set slack.username=Velero \
  --set discord.enabled=true \
  --set discord.failures_only=false \
  --set discord.webhook=https://... \
  --set discord.mentions.enabled=false \
  --set discord.mentions.failures_only=false \
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


## Different options explained
#### *.failures_only
* when set to true (default false), notifications of backups with status "Completed" are not send/received.

#### Partially_failed_count_as_completed
* when set to true (default false), backups with status "PartiallyFailed" are perceived as completed. This means that no notifications are send/received when the option *.failures_only is set to true."


## Quick guide on how to integrate with
* webhook (azure logic app, [healthchecks.io)](https://healthchecks.io/))
* discord webhook
...

## License

[MIT License](https://github.com/vitobotta/velero-notifications/blob/main/LICENSE)

