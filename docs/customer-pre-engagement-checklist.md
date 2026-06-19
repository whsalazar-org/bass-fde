# Customer Pre-Engagement Checklist

**Audience:** Customers preparing for an FDE engagement.

Complete all items on this checklist **before** your FDE engagement kicks off. The FDE team's time is reserved for deep, embedded Copilot adoption work, not provisioning, licensing, or infrastructure setup. Arriving ready means arriving fast.

> **Not sure if you're ready?** Share this checklist with your GitHub account team before the engagement is scheduled. Items marked incomplete are conversations to have _now_, not on Day 1.

## Section 1: GitHub Enterprise Cloud: Foundation

- [ ] **GitHub Enterprise is provisioned and configured:** your enterprise and organization are set up on GitHub (GHEC, GHEC with data residency, or EMU preferred; GHES supported but may limit some Copilot features)
- [ ] **GitHub organization(s) are set up:** repos, teams, and org structure reflect your real development environment
- [ ] **Admin access is confirmed:** at least one internal GitHub org admin is available and reachable during the engagement
- [ ] **Single Sign-On (SSO) / SAML is configured** (if applicable): developers can authenticate without blockers
- [ ] **Network access is resolved:** VPN, firewall, or proxy rules that affect GitHub.com are understood and documented (self-hosted runner configurations, outbound access policies, etc.)

## Section 2: GitHub Copilot: Licensing & Enablement

- [ ] **GitHub Copilot licenses are purchased and assigned:** all target developers have active Copilot seats (confirm whether Enterprise or Business tier, as feature availability differs)
- [ ] **Copilot is enabled in the target organization(s),** or at the enterprise level for all organizations, and feature toggles are on, not just licenses assigned
- [ ] **Key Copilot features are enabled**, at minimum:
  - [ ] Copilot Chat
  - [ ] Copilot Cloud Agent (CCA)
  - [ ] Copilot Code Review (CCR)
  - [ ] Copilot in the CLI (`gh copilot`)
  - [ ] Editor integration (VS Code, JetBrains, etc.)
- [ ] **Any content exclusions are documented**: you know which directories or repositories Copilot should not access (even if not yet configured in settings)
- [ ] **Developers have installed the Copilot extension** in their primary IDE before Day 1 and FDE team is aware of the primary IDE(s) and versions used by developers
- [ ] **Model policies are reviewed** (if applicable): confirm which models are enabled for your organization and that any advanced models (e.g., Claude/Opus, Gemini) are approved by your security team
- [ ] **Billing and budgets are configured:** understand your Copilot premium request usage (PRUs) and GitHub Actions minutes allocation, and set spending limits or budgets to avoid interruptions during the engagement

## Section 3: People & Stakeholders: Engagement Readiness

- [ ] **An internal champion is identified:** a senior developer or tech lead who will actively pair with the FDE team and own adoption post-engagement
- [ ] **1-3 target engineering teams are identified:** teams that will actively participate, with engineers who have capacity to dedicate time during the engagement window and an active-development project that can be used for implementing Copilot practices
- [ ] **An executive sponsor is named:** someone with authority to unblock obstacles and support adoption goals
- [ ] **Participant engineers have cleared their calendars:** the engagement window is protected time, not squeezed between competing priorities
- [ ] **Internal security/legal approval for AI tooling is complete:** AI policy approvals should cover both the use of Copilot itself and any advanced models your organization plans to enable (e.g., Claude/Opus, Gemini)

## Section 4: Repositories & Codebases: Access & Readiness

- [ ] **Target repositories are identified:** 1-3 repos where the FDE team will observe and guide your engineers through real workflows
- [ ] **Repositories are on GitHub with active development:** teams are fully using the GitHub platform for their day to day development work
- [ ] **GitHub Actions is enabled** in the target organization(s): CCA and Copilot Code Review (agentic capabilities) both require Actions to run
- [ ] **Runner strategy is decided:** both CCA and CCR can use GitHub-hosted or self-hosted runners, and if using self-hosted runners, confirm they are configured for use with [CCA](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/customize-the-agent-environment#using-self-hosted-github-actions-runners) and [CCR](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review/configure-runners)
- [ ] **Teams have approval to modify the selected repositories** as part of the engagement

## Section 5: Engagement Scope: Aligned Before Day 1

- [ ] **A specific adoption goal is articulated.** For example: _"Enable CCA and CCR for our platform team"_ or _"Move our 3 squads from Copilot Chat-only to using Cloud Agent"_, not _"improve Copilot adoption generally"_
- [ ] **Success criteria are agreed upon:** 2-4 measurable outcomes that define a successful engagement (e.g., "Reach 60% Copilot MAU across 2 teams" or "Enable CCA on 5 active repositories")
- [ ] **The engagement is scoped to Copilot:** any non-Copilot work is either completed in advance or explicitly agreed as out of scope
- [ ] **A real-time communication channel is set up:** Slack, Teams, or equivalent where the FDE team and customer engineers will collaborate during the engagement

## Out of Scope: Complete These _Before_ the Engagement

The following activities are **not FDE work**. If these are incomplete at kickoff, engagement time will be spent on setup instead of Copilot adoption.

| ❌ Not FDE Scope | ✅ What to Do Instead |
|---|---|
| Migrating CI/CD pipelines to GitHub Actions | Engage Expert Services or Partners before the FDE engagement |
| Setting up GitHub Enterprise Cloud from scratch | Work with your AE/SE to complete GHEC provisioning first |
| Resolving internal security or compliance approvals for AI tooling | Get internal AI policy approvals in place before kickoff |
| Procuring or assigning Copilot licenses | Complete licensing via your GitHub account team before Day 1 |
| Onboarding developers to GitHub basics (PRs, Issues, Actions) | Developers should be comfortable with core GitHub workflows before the FDE arrives |
| Migrating the work-related repositories to GitHub | Engage Expert Services or Partners before the FDE engagement |
