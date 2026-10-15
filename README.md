# Enterprise Contact Automation System with n8n

An enhanced contact-management automation concept built in n8n. It receives contact submissions through a webhook, evaluates validation conditions, prepares contact data, routes inquiries by category, logs records in Google Sheets, and connects email and Telegram notifications.

## Overview

The workflow is designed to demonstrate a more structured inbound-contact process, including a conditional validation step before downstream processing.

### Intended Flow

1. **Webhook** — receives a `POST` request.
2. **If** — evaluates conditions for required contact fields and message content.
3. **prepare_data** — maps the contact fields and timestamp.
4. **Switch** — routes requests by subject:
   - Booking
   - Career
   - Complaint
   - General
   - Partnership
5. **Google Sheets** — appends contact details to a worksheet.
6. **Telegram and Gmail** — provide notifications and an acknowledgement email.
7. **Respond to Webhook** — provides a response on the alternate branch.

## Tech Stack

- n8n workflow automation
- Webhooks and JSON
- Conditional logic
- Google Sheets
- Gmail
- Telegram Bot API

## Example Request

```json
{
  "user_name": "Jane Doe",
  "user_email": "jane@example.com",
  "phone": "+1-555-0100",
  "subject": "General",
  "message": "I have a question about your services."
}
```

## Setup

1. Import `workflow.json` into your n8n instance.
2. Configure a new webhook URL.
3. Connect your own Google Sheets, Gmail, and Telegram credentials.
4. Replace placeholder recipient IDs and spreadsheet references with your own settings.
5. Review the If node's conditions and connect its true/false outputs to the intended next steps.
6. Check that the validation logic matches the incoming JSON schema.
7. Review all Switch rules and confirm category-to-action mappings.
8. Test valid, invalid, missing-field, and unknown-subject submissions before activation.

## Security Notes

The included export has been sanitized for public sharing. Credentials and destination identifiers must be configured in your own n8n instance. Never commit tokens, OAuth secrets, private webhook URLs, or real contact records.

## Validation and Testing Status

This repository represents an exported workflow design, not a claim of production readiness. The supplied workflow contains configuration details that should be reviewed before deployment:

- The If node's true branch should be checked to ensure it reaches `prepare_data`; the provided connections do not show that connection.
- Review each If condition, especially the email/message-count condition, to confirm that its operator, value types, and expressions match the intended validation rule.
- Review the Switch rules: some conditions appear to use fixed text rather than the incoming `Subject` field.
- Confirm the webhook response code and response behavior are appropriate for your client.

## Future Improvements

- Define a clear validation schema and consistent error responses.
- Add a fallback branch for unsupported categories.
- Add duplicate detection, spam protection, and rate limiting.
- Add retries, error workflows, and monitoring.
- Create test cases for valid and invalid submissions.

## License

Choose and add a license before publishing. An MIT license is one option if you intend to permit reuse under those terms.
