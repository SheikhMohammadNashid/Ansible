
In Ansible, the `-v` flag stands for **verbose**. Adding more `v`s increases the detail level of the output that Ansible prints to your terminal while running a playbook. It is the primary tool for debugging when tasks are failing or not behaving the way you expect.

Here is exactly what each level reveals:

|**Flag**|**Verbosity Level**|**What it actually shows you**|
|---|---|---|
|**`-v`**|Level 1|**Task results.** It shows the basic output of completed tasks, including the specific changes made on the target machine or extra details about a skipped task.|
|**`-vv`**|Level 2|**Task inputs.** In addition to Level 1, it prints the specific arguments and variables being passed into the task module, helping you spot syntax or variable errors.|
|**`-vvv`**|Level 3|**Connection details.** This opens up the communication layer. It shows how Ansible is connecting to the remote machine (usually via SSH), including the exact commands it is executing under the hood.|
|**`-vvvv`**|Level 4|**Connection debugging.** This is the maximum depth. It outputs raw SSH connection details, plugin loading information, and internal script paths. It is quite spammy and usually only needed for complex network or SSH keys troubleshooting.|

### Quick Summary of when to use which:

- If a task fails and you just want a bit more context, start with **`-v`**.
    
- If you suspect a variable isn't passing correctly into a task, use **`-vv`**.
    
- If Ansible is hanging or failing to connect to your remote server at all, jump straight to **`-vvv`**.

Check before running the playbook

### 1. `--syntax-check` (The Structural Test)

This flag reads through your playbook, inventory, and role files to ensure the YAML syntax is valid and that Ansible can actually parse the instructions.

- **What it does:** It runs a purely static analysis. It checks for misplaced indentation, missing colons, typos in Ansible keywords, or unclosed quotes.
    
- **Does it touch the servers?** No. It runs entirely on your local machine and never connects to your target hosts.
    
- **When to use it:** Use this as a quick sanity check right after writing or editing a playbook to catch basic typos before running anything.
    

> **Command Example:**
> 
> `ansible-playbook playbook.yml --syntax-check`

### 2. `-C` or `--check` (The Dry Run)

This flag is Ansible’s **"Dry Run"** mode. It simulates the execution of your playbook to show you what _would_ change without actually changing anything on your servers.

- **What it does:** Ansible connects to your remote servers, checks their current state, and reports back whether tasks would return `ok` (no change needed), `changed` (it would modify something), or `failed`.
    
- **Does it touch the servers?** Yes, it connects to them via SSH to read their current state, but it **does not make any modifications**.
    
- **When to use it:** Use this before deploying to production to ensure your playbook won't accidentally overwrite important configurations or restart services unexpectedly.
    

> **Command Example:**
> 
> `ansible-playbook playbook.yml -C`

### Summary: The Difference at a Glance

| **Feature**           | **--syntax-check**                                | **-C / --check**                                           |
| --------------------- | ------------------------------------------------- | ---------------------------------------------------------- |
| **Focus**             | Code structure & YAML rules.                      | Expected real-world impact.                                |
| **Server Connection** | **No.** Local execution only.                     | **Yes.** Connects to remote hosts.                         |
| **What it catches**   | Bad indentation, typos in modules, syntax errors. | Missing packages, configuration drift, potential failures. |
| **Modifies System?**  | No.                                               | No.                                                        |