# AgentCrash Lab

**Break it before your users do.**

AgentCrash Lab is an experimental AI-agent testing project built with n8n. It evaluates simulated support-agent responses against predefined checks to identify common reliability and safety failures.

## Project Overview

The project contains two n8n workflows:

1. **Support Agent** — simulates support-agent behavior across normal and intentionally faulty scenarios.
2. **Test Runner** — sends test cases to the support agent, evaluates the responses, and generates an HTML report.

## Test Scenarios

| Test ID | Scenario | What it checks |
|---|---|---|
| ACL-001 | Normal | Valid baseline response |
| ACL-002 | Hallucination | Refund claims stay within the 30-day policy |
| ACL-003 | Missing information | Agent handles a missing order ID safely |
| ACL-004 | Invalid output | Required response fields are present |
| ACL-005 | Duplicate action | Action IDs are not reused |
| ACL-006 | Tool failure | Agent does not report success after a tool failure |

## Test Results

Two test runs were completed:

| Mode | Passed | Failed | Pass rate |
|---|---:|---:|---:|
| Buggy | 1/6 | 5 | 17% |
| Fixed | 6/6 | 0 | 100% |

In buggy mode, the test runner detected five deliberately simulated issues. In fixed mode, all six configured checks passed.

## Project Structure

```text
AgentCrash Lab/
├── workflows/
│   ├── 1-ACL-Demo-Support-Agent.json
│   └── 2-ACL-AgentCrash-Test-Runner.json
├── reports/
│   └── agentcrash-report.html
└── README.md
```

## Requirements

- Docker Desktop
- n8n
- A web browser

## Running the Project

1. Start your local n8n instance.
2. Import `1-ACL-Demo-Support-Agent.json` from the `workflows` folder.
3. Publish or activate the support-agent workflow.
4. Import `2-ACL-AgentCrash-Test-Runner.json`.
5. Ensure the test runner's HTTP Request URL points to the support-agent webhook.
6. Set `MODE` to `"buggy"` or `"fixed"` in the **Generate Test Suite** node.
7. Execute the test runner and inspect the **Build Report** output.
8. Open the generated HTML report in a browser.

## Tech Stack

- n8n
- Docker
- JSON
- JavaScript
- HTTP webhooks
- HTML and CSS

## Limitations

This project uses a simulated support agent and six predefined test scenarios. Passing these checks does not establish that a real AI agent is safe or reliable in every situation.

## Future Improvements

- Add more test scenarios and edge cases.
- Expand output-schema validation.
- Add more robust duplicate-action tracking.
- Integrate a real AI agent for controlled evaluations.
- Improve report storage and execution history.

---

**Author:** Ch Usman Elahi  
**Project:** AgentCrash Lab.