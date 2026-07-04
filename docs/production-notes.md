# Production Notes

- Keep copyright and commercial-use review in the publishing workflow.
- Store composition_plan and output settings with task_id.
- Use webhooks for music jobs in automated creator pipelines.
- Store `data.task_id` immediately after submit.
- Use polling for local tests and `callback_url` webhooks in production.
- Handle `failed` status as a normal product state, not an unexpected crash.
- Keep `POYO_API_KEY` on the server.
- Do not log full prompts if they may contain user-private data.

## Security Checklist

- Never expose `POYO_API_KEY` in browser code, mobile apps, screenshots, or public logs.
- Use environment variables or a secret manager for API keys.
- Use allowlisted webhook endpoints when callbacks are enabled.
- Store request metadata separately from sensitive user content when possible.
