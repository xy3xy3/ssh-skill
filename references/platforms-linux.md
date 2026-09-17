# Linux Invocation

Resolve `<SSH_SKILL_ROOT>` from the loaded skill, then invoke the unified CLI.

Use `.venv/bin/python` for the CLI. Prefer `uv venv .venv` and
`uv pip install --python .venv/bin/python paramiko`; otherwise use
`python3 -m venv .venv` and `.venv/bin/python -m pip install paramiko`.
Never use a bare global `pip`.

```bash
.venv/bin/python "<SSH_SKILL_ROOT>/scripts/ssh_skill.py" doctor --json
.venv/bin/python "<SSH_SKILL_ROOT>/scripts/ssh_skill.py" exec example-host "hostname"
.venv/bin/python "<SSH_SKILL_ROOT>/scripts/ssh_skill.py" upload example-host "./app.tar.gz" "/tmp/app.tar.gz"
```

- OpenSSH and `ssh-add` are discovered from PATH.
- Keep remote paths in POSIX form.
- Keep the remote command as one process argument.
- Do not add a nested shell command string.
- `SSH_AUTH_SOCK` is used only for local agent diagnosis.
- Parse the single stdout result separately from optional real-time JSONL
  progress on stderr.

Use the distribution's package manager only when doctor reports a missing
dependency and the user has authorized installation. Python 3.10-3.13 is the
tested release range.
