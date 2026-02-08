# Agent User Skill for Microsoft Entra ID

## Overview

This skill provides comprehensive guidance on **creating Agent Users in Microsoft Entra ID** from Agent Identities. It enables AI agents to act as digital workers with full user identity capabilities in Microsoft 365 and Azure environments.

## What is an Agent User?

An **Agent User** is a specialized user identity in Microsoft Entra ID that allows AI agents to:

- **Access user-specific APIs and services** (Exchange mailboxes, Teams, org charts, etc.)
- **Receive tokens with `idtyp=user`** instead of the typical application token (`idtyp=app`)
- **Act as digital workers** within your organization while maintaining security boundaries
- **Participate in Teams**, access calendars, send emails, and appear in organizational charts

Unlike regular service principals or app registrations, Agent Users bridge the gap between application identities and user-like operations.

## Key Features

✅ **Step-by-step Instructions** - Detailed guide from verification to license assignment  
✅ **Multiple Methods** - HTTP API requests and PowerShell examples  
✅ **Prerequisites Checklist** - Clear requirements and permissions needed  
✅ **Troubleshooting Guide** - Common errors and solutions  
✅ **Architecture Overview** - Visual representation of agent identity relationships  
✅ **Provisioning Timelines** - Expected wait times for various Microsoft 365 services  

## Quick Start

### Prerequisites

- Microsoft Entra tenant with Agent ID capabilities
- An existing agent identity (service principal of type `ServiceIdentity`)
- Required permissions: `AgentIdUser.ReadWrite.IdentityParentedBy` (or `AgentIdUser.ReadWrite.All` or `User.ReadWrite.All`)
- Agent ID Administrator role (minimum)

### Basic Usage

1. **Verify your agent identity exists** and is of type `agentIdentity`
2. **Create the agent user** with required properties (display name, UPN, etc.)
3. **Optional**: Assign a manager for org chart visibility
4. **Optional**: Set usage location and assign licenses for mailbox/Teams access

For detailed step-by-step instructions, see **[SKILL.md](./SKILL.md)**.

## What Agent Users Can Do

| Capability | Supported |
|---|---|
| Access user-only APIs with `idtyp=user` tokens | ✅ |
| Own a mailbox, calendar, and contacts | ✅ |
| Participate in Teams chats and channels | ✅ |
| Appear in org charts and People search | ✅ |
| Be added to Microsoft Entra groups | ✅ |
| Be assigned licenses | ✅ |
| Have passwords or interactive sign-in | ❌ |
| Be assigned privileged admin roles | ❌ |
| Be added to role-assignable groups | ❌ |

## Architecture

```
Agent Identity Blueprint (application template)
    │
    ├── Agent Identity (service principal - ServiceIdentity)
    │       │
    │       └── Agent User (user - agentUser) ← 1:1 relationship
    │
    └── Agent Identity Blueprint Principal
```

**Key Relationship**: Each agent identity can have **exactly one** agent user (1:1 relationship).

## Documentation Structure

- **README.md** (this file) - Overview and quick reference
- **[SKILL.md](./SKILL.md)** - Complete detailed implementation guide with:
  - Prerequisites and permissions
  - Step-by-step instructions with HTTP and PowerShell examples
  - Manager assignment and license configuration
  - Provisioning timelines
  - Troubleshooting guide
  - Official Microsoft documentation references

## Security Considerations

🔒 **Agent Users have security constraints**:
- Cannot have passwords, passkeys, or perform interactive sign-in
- Cannot be assigned privileged admin roles
- Cannot be added to role-assignable groups
- Have permissions similar to guest users by default
- Authentication happens through the parent agent identity's credentials

## Common Use Cases

- **AI assistants** that need to send emails or schedule meetings
- **Automation agents** that require user-level access to Microsoft 365
- **Digital workers** participating in Teams conversations
- **Service accounts** that need to appear as users in organizational structures
- **Bots** that need access to user-specific Graph API endpoints

## Troubleshooting

Common issues and quick fixes:

| Issue | Solution |
|---|---|
| "Agent user IdentityParent does not exist" | Verify the `identityParentId` points to an `agentIdentity` service principal |
| "400 Bad Request" (already linked) | Each agent identity supports only one agent user |
| "409 Conflict" on UPN | Use a unique `userPrincipalName` |
| License assignment fails | Set `usageLocation` before assigning licenses |

For more detailed troubleshooting, see [SKILL.md](./SKILL.md#troubleshooting).

## Official Microsoft Documentation

- [Agent identities](https://learn.microsoft.com/en-us/entra/agent-id/identity-platform/agent-identities)
- [Agent users](https://learn.microsoft.com/en-us/entra/agent-id/identity-platform/agent-users)
- [Create agentUser (Graph API)](https://learn.microsoft.com/en-us/graph/api/agentuser-post?view=graph-rest-beta)
- [agentUser resource type](https://learn.microsoft.com/en-us/graph/api/resources/agentuser?view=graph-rest-beta)

## Contributing

This is a documentation skill repository. Contributions to improve clarity, add examples, or update with the latest Microsoft Entra ID features are welcome.

## License

This documentation is provided as-is for educational and reference purposes.

---

**Need detailed implementation steps?** → See **[SKILL.md](./SKILL.md)** for the complete guide.
