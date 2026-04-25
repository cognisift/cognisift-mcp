CogniSift

An autonomous forensic investigation assistant powered by Claude and the Model Context Protocol (MCP).

Hackathon submission: Find Evil!  |  Status:  In active development
What is CogniSift?
CogniSift gives Claude the ability to investigate compromised systems on its own. Instead of a human analyst spending hours running memory and disk forensic tools by hand, Claude calls those tools through a custom MCP server, correlates the findings, and reports what happened — all while operating under a strict read-only security boundary that guarantees evidence is never modified.
The goal: prove that an AI agent can perform a real forensic investigation with zero spoliation of evidence and a full, auditable trail of every action it took.
How it works

┌──────────┐      ┌──────────────┐      ┌────────────────┐      ┌──────────────┐
│  Analyst │ ───▶ │  Claude Code │ ───▶ │   MCP Server   │ ───▶ │  SIFT Tools  │
│  (You)   │      │   (Brain)    │      │ (Read-only API)│      │ Volatility,  │
└──────────┘      └──────────────┘      └────────────────┘      │    Plaso     │
                                                                 └──────────────┘
                                          ▲
                                          │
                                  All actions logged
                                  to execution_traces.json




Architecture diagram coming in architecture.png — see Phase 4 of the project plan.


Why this matters
In digital forensics, modifying evidence makes it inadmissible. Most AI-tool integrations let the model do anything its tools allow — including destructive actions. CogniSift inverts this: the MCP server's wrapper functions are the only path between Claude and the underlying tools, and those wrappers physically cannot perform write or delete operations. The security boundary lives in code, not in the prompt.
Project status
This project is being built across five phases between April and June 2026. The current state of the repo reflects active work in progress.
PhaseStatusFocus1. Environment & repo setup🟡 In progressVMs, GitHub structure, dependencies2. Core engine & audit trail⬜ Not startedMCP server, Volatility wrapper, auto-logger3. Deep correlation & datasets⬜ Not startedPlaso wrapper, cross-tool correlation4. Agent logic & accuracy report⬜ Not startedChain-of-thought prompting, zero-spoil testing5. Demo video & final polish⬜ Not startedSubmission package.

Repository layout
The folder structure will grow as the project develops. Final layout:

cognisift-mcp/
├── README.md               # This file
├── LICENSE                 # MIT
├── architecture.png        # System diagram (Phase 4)
├── src/                    # MCP server + tool wrappers
│   ├── mcp_server.py
│   └── wrappers/
├── docs/                   # Accuracy report, dataset documentation
└── logs/                   # Auto-generated execution traces











Team

Ruthless — "Documentation & forensic analysis" — @unpatchedxyz
Additional teammates to be added

License
This project is licensed under the MIT License — see the LICENSE file for details.
Acknowledgments

SANS SIFT Workstation — the forensic toolkit this project is built on
Volatility Foundation — memory forensics framework
Plaso (log2timeline) — disk timeline analysis
Anthropic Model Context Protocol — the bridge between Claude and external tools
