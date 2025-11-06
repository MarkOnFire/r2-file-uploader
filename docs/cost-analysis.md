# Overhead Cost Analysis

## Assumptions
- 30 guest uploads per month.
- Average file size: 120 MB (voice memo length ~60 minutes).
- Files retained for 6 months before archival, yielding ~21.6 GB stored at steady state (30 × 0.12 GB × 6).
- Each upload uses ~5 Worker API requests (init, signed parts, completion) plus 1 admin email.
- Guests download their own submissions once; admins retrieve 3× per asset on average.

## Cloudflare Stack Costs
### R2 Storage & Operations
- Free tier provides 10 GB storage, 1 M Class A ops, 10 M Class B ops, and free egress for Standard storage (`knowledge/costs/r2-pricing.md:189`, `knowledge/costs/r2-pricing.md:195`, `knowledge/costs/r2-pricing.md:197`).
- Above the free tier: $0.015 / GB-month for Standard storage; $4.50 / M Class A and $0.36 / M Class B (`knowledge/costs/r2-pricing.md:165`, `knowledge/costs/r2-pricing.md:177`).
- Scenario cost:
  - Stored data: (21.6 GB − 10 GB) × $0.015 ≈ **$0.17/month**.
  - Operations: ~180 Class A (init/complete) and ~180 Class B (status checks/download metadata) per month ⇒ well under free allowances.
  - Egress: free for both internal and guest downloads (`knowledge/costs/r2-pricing.md:170`, `knowledge/costs/r2-pricing.md:182`).

### Cloudflare Workers & Email
- Workers Free plan covers 100 k requests/day with 10 ms CPU time per invocation (`knowledge/costs/workers-pricing.md:414`, `knowledge/costs/workers-pricing.md:417`, `knowledge/costs/workers-pricing.md:457`).
- Our workload (~180 requests/month) is negligible, so **$0** expected spend.
- Email Routing bindings leverage verified destination addresses without explicit per-email fees in the referenced docs; usage remains within free tier expectations (`knowledge/cloudflare-email/email-workers.md:72`, `knowledge/cloudflare-email/email-workers.md:103`, `knowledge/cloudflare-email/email-workers.md:135`).

**Cloudflare total (Scenario)**: ≈ **$0.17/month** once storage exceeds the free 10 GB; otherwise $0.

## Alternative Stacks
### Amazon S3 + Lambda/SES
- S3 bills for storage based on class and charges for operations and data transfer (`knowledge/alternatives/aws-s3-pricing.md:87`, `knowledge/alternatives/aws-s3-pricing.md:97`).
- Public egress runs $0.005–$0.015 / GB (region-dependent), so 30 internal/admin downloads (≈3.6 GB) would add **$0.02–$0.05** monthly (`knowledge/alternatives/aws-s3-pricing.md:209`, `knowledge/alternatives/aws-s3-pricing.md:244`, `knowledge/alternatives/aws-s3-pricing.md:270`).
- Additional costs: Lambda invocations, SES outbound email, and CloudFront/CDN charges, each adding fractional dollars but increasing operational complexity.
- **Trade-off**: Mature ecosystem and richer tooling, but higher egress charges and more infrastructure to manage for comparable workloads.

### Backblaze B2 + Functions
- Published rates: $6/TB-month (~$0.006/GB-month) storage and free egress up to 3× monthly average, then $0.01/GB (`knowledge/alternatives/backblaze-b2-pricing.md:62`, `knowledge/alternatives/backblaze-b2-pricing.md:64`, `knowledge/alternatives/backblaze-b2-pricing.md:68`, `knowledge/alternatives/backblaze-b2-pricing.md:104`).
- Scenario cost: (21.6 GB × $0.006) ≈ **$0.13/month** with egress remaining free if total downloads < 64.8 GB (3× storage).
- Requires separate compute (e.g., Cloudflare Worker still possible via S3-compatible API) but lacks built-in email routing.

## Recommendation
- **Cloudflare-first architecture** keeps upload, storage, and notification in one platform with negligible cost at current scale (<$0.20/month) and the simplest operational footprint.
- Monitor storage growth; if library exceeds ~250 GB, revisit costs to compare against B2’s lower storage rate or hybrid strategies.
- Reconsider alternatives only if:
  - You require cross-cloud redundancy or advanced processing (S3 ecosystem).
  - Storage scales into multi-terabyte ranges where $0.006/GB (B2) materially outperforms R2 and free egress tiers are fully utilized.
