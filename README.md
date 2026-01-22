# Zendesk Integrations

This repo contains Zendesk private apps and supporting AWS Lambdas used by Swanson Health Products.

## Structure

- `apps/cxone-lookup-app/` - CXone caller/requester lookup app (Zendesk private app)
- `apps/promo-lookup-app/` - Promo/source offer lookup app (Zendesk private app)
- `apps/shopify-lookup-app/` - Shopify customer lookup app (Zendesk private app)
- `lambda/cxone-bridge/` - AWS Lambda bridge for CXone active-call lookups
- `lambda/shopify-lookup/` - AWS Lambda that queries Shopify Admin API (via GraphQL) for customer lookup

## Notes

- Apps are deployed to Zendesk via `zcli` from each app folder (`zcli apps:update` or `zcli apps:package` + upload).
- Lambda deployments are performed via AWS (CLI or Console). `lambda/shopify-lookup/` requires bundling dependencies (AWS SDK v3 client) with the deployment artifact.
- Do not commit credentials. Zendesk app settings (API base URLs, API keys) are configured in Zendesk Admin. Shopify tokens should be stored in AWS Secrets Manager and read by the Lambda at runtime.
