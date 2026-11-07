# Python — Learning Curve, With an Ops Accent

Scripts and notes from working through Python fundamentals — kept exactly as I learned, so the progression is honest. What makes this repo more than `print("hello")` drills is that the exercises lean toward ops problems: provisioning users, checking files, deploying a website.

## The fundamentals

| File | What it drills |
|---|---|
| `Variables.py`, `Dataypes.py` | Names, types (yes, the typo in the filename is original) |
| `Operators.py`, `Condition_vars.py`, `Conditions.py` | Expressions and branching |
| `Loops.py`, `Loop2.py`, `Break And Continue.py`, `Break Exxample.py` | Loop control |
| `Printing.py`, `QuotesAndComments.py` | Output and style |
| `Functions.py`, `Functions2.py` | Defining and calling |
| `Slicing.py` | Sequence slicing |
| `kwargs.py`, `Variable Lenght Arguments.py`, `modern.py` | `*args` / `**kwargs` |
| `Built-in Methods.py`, `Learn-JSON.json` | Stdlib + JSON round-trip |
| `bash-sytax.sh`, `python-syntaxx.py` | The same logic side by side, bash vs Python |

`modern.py` is the fun one: `time_activity(*args, **kwargs)` sums minutes and spends a random extra on a random activity; `vac_feedback()` maps an efficacy number to a verdict.

## The ops-flavored part

**`ostasks/ostasks.py`** — the best file in the repo. It provisions users idempotently in ~40 lines of stdlib:

```python
exitcode = os.system("id {}".format(user))
if exitcode != 0:
    os.system("useradd {}".format(user))     # only if missing
...
if os.path.isdir("/opt/science_dir"):
    print("Directory already exist, skipping it")
else:
    os.mkdir("/opt/science_dir")
```

Check → act → skip if done. I didn't know the word "idempotent" yet; the script already was. `check-file.py` is the smaller sibling.

**`Playbook.YAML`** — technically not Python at all: my first Ansible playbook, living here because the course handed it out mid-Python. Two hosts (`websrvgrp` gets httpd + a config copy, `dbsrvgrp` gets PostgreSQL). It's the bridge between the bash scripts in [Bash-scripting](https://github.com/amanvicky/Bash-scripting) and real config management.

**`fabric/`** — a Fabric experiment: `fabfile.py` drives a deployment, with a Tooplate static site (wave-cafe) as the thing being deployed. Same deploy pattern my bash `websetup` scripts automate — this time from Python.

## Run

```bash
python "Slicing.py"        # any file — most are self-contained demos
python ostasks/ostasks.py  # the provisioning script (wants a Linux box)
```

## Where the journey went

The deployment theme continues up the automation ladder: [cloudformation-practice](https://github.com/amanvicky/cloudformation-practice) (cfn-init), [Jenkins-CI-CD](https://github.com/amanvicky/Jenkins-CI-CD) (pipelines), [kubernetes](https://github.com/amanvicky/kubernetes) (objects in a real cluster). The current-day work — AI agents and computer vision — lives in [Genesis](https://github.com/amanvicky/Genesis-Business-Decoding-Engine) and [Open-Broadcast](https://github.com/amanvicky/Open-Broadcast).
