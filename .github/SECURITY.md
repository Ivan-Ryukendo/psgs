# Security policy

psgs is a set of instructions for coding agents. A security problem here usually takes one of these forms:
- an instruction that could make an agent weaken security, leak a secret, or run something without asking;
- a recommended third-party skill or package that turns out to be malicious or compromised;
- a way for repository or web content to override psgs's rules (prompt injection).

## Reporting
Please report privately. Use **GitHub → Security → Report a vulnerability** on this repo, which opens a private advisory. Don't open a public issue for a vulnerability.

Include the file and line, what an agent would do, and how to reproduce it. Never include real secrets.

You can expect an acknowledgement within 7 days. Fixes are released as a new version, with a CHANGELOG entry and credit if you want it.

## Supported versions
Only the latest release gets fixes.
