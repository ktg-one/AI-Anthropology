---
name: ktg-content-automation
description: Automated content pipeline using n8n workflows for social media, blog posts, and outreach. Use when building content automation, creating posting schedules, automating social media, setting up email sequences, or implementing "clone mode" where user approves rather than creates. Integrates with n8n-workflow-patterns skill for workflow generation.
---

# KTG Content Automation

Automated content pipeline achieving "clone mode" - user approves, not creates.

## Core Architecture

```
Calendar Trigger → Draft Generation → Review Queue → Auto-Post → Monitor
```

## Clone Mode Pipeline

### Stage 1: Triggers

| Trigger | Source | Action |
|---------|--------|--------|
| Calendar | Notion/Airtable | Fires on scheduled content slot |
| RSS | Blog/News feeds | Fires on new content to repurpose |
| Webhook | External events | Fires on engagement opportunities |
| Manual | User request | Fires immediate content need |

### Stage 2: Draft Generation

Webhook receives trigger → Claude generates draft → PR created in repo.

**n8n Workflow Pattern**: `references/draft-generation-workflow.json`

### Stage 3: Review Queue

- Drafts land in review channel (Slack/Discord/Email)
- User has 10min review window
- Approve = auto-post
- Reject = flag for revision

### Stage 4: Distribution

Approved content → parallel post to:
- X (Twitter)
- LinkedIn
- Reddit (subreddit-specific)
- Blog (if long-form)

### Stage 5: Monitoring

Grok4 watches:
- Sentiment score
- Engagement spikes
- Competitor mentions
- Response opportunities

## Workflow Templates

### Content Calendar Automation

See `assets/content-calendar-workflow.json` for n8n import.

**Pattern**: Schedule → Fetch slot → Generate draft → Create PR → Notify

### Social Distribution

See `assets/social-distribution-workflow.json` for n8n import.

**Pattern**: Webhook (approval) → Parallel branches → Post to each platform → Log results

### Engagement Monitor

See `assets/engagement-monitor-workflow.json` for n8n import.

**Pattern**: Schedule (hourly) → Fetch mentions → Score sentiment → Alert if threshold

## Integration Points

### With n8n-workflow-patterns

This skill uses patterns from n8n-workflow-patterns:
- Webhook Processing for draft triggers
- Scheduled Tasks for calendar-based posting
- HTTP API Integration for social platforms

### With n8n MCP Tools

Use n8n MCP tools for:
- `search_nodes` - Find platform-specific nodes
- `validate_workflow` - Verify before activation
- `get_template` - Reference existing patterns

### With ktg-memory-compress

Save content pipeline state across sessions using CEP carry-packets.

## Content Types

### X Thread

- Hook (problem/insight)
- 3-5 body tweets
- CTA with link
- **Template**: `assets/x-thread-template.md`

### LinkedIn Post

- Professional hook
- Story/insight
- Lesson learned
- CTA
- **Template**: `assets/linkedin-template.md`

### Reddit Post

- Subreddit-appropriate title
- Value-first content
- Soft CTA
- **Template**: `assets/reddit-template.md`

### Blog Post

- SEO title
- Hook paragraph
- Structured content
- CTA
- **Template**: `assets/blog-template.md`

## Scheduling Strategy

| Day | Content Type | Platform |
|-----|--------------|----------|
| Monday | Technique deep-dive | Blog → X thread |
| Wednesday | Case study | LinkedIn → Reddit |
| Friday | Community response | X → Reddit |

## Clone Mode Checklist

- [ ] Content calendar populated (2 weeks ahead)
- [ ] n8n workflows active
- [ ] Review channel configured
- [ ] Distribution credentials set
- [ ] Monitoring alerts enabled
- [ ] Approval window defined (default: 10min)

## Quick Start

1. Import `assets/master-workflow.json` to n8n
2. Configure credentials for platforms
3. Set calendar source (Notion/Airtable)
4. Configure review channel
5. Activate workflows
6. You now approve, not create
