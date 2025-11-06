# OpenConfig Ansible Collection – Developer & Contributor Guide

Thank you for your interest in improving the **`nokia.openconfig`** Ansible collection!
This guide explains how to set up your development environment, run tests, and contribute changes — following the [Ansible Community Guidelines](https://docs.ansible.com).

---

## Overview

The `nokia.openconfig` collection provides network automation support for Nokia **SR OS** devices through **CLI** and **NETCONF** interfaces.
Developers can use the included `run.sh` helper script to simplify local development, containerlab deployment, and regression testing.

---

## Prerequisites

Before contributing, ensure your environment includes:

* **Python 3.11 or newer**
* **Ansible Core 2.13 or newer** (recommended)
* **Docker** for running SR OS container images
* **Access** to SR OS and SRLinux container images and a valid license file
* A Linux, macOS, or BSD-like system with common GNU tools (`bash`, `curl`, `make`, etc.)

---

## Quick Start

### 1. Set up a Python virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

### 2. Clone the repository

```bash
git clone https://github.com/nokia/openconfig-ansible-collection.git
```

### 3. Build and Install collection locally

```bash
cd openconfig-ansible-collection
pip install -r requirements.txt

cd plugins/utils
python -m grpc_tools.protoc -I . --python_out=. --grpc_python_out=. *.proto
sed -i 's/^import \(.*_pb2\)/from ansible_collections.nokia.openconfig.plugins.utils import \1/' *
cd ../..

ansible-galaxy collection install . --force
```

### 4. Install runtime dependencies

Install required Ansible collections

```bash
ansible-galaxy collection install ansible.netcommon
ansible-galaxy collection install nokia.srlinux nokia.sros
```

Install [containerlab](https://containerlab.dev):

```bash
bash -c "$(curl -sL https://get.containerlab.dev)"
```

### 5. Prepare images and licenses

Pull `nokia_sros` and `nokia_srlinux` container images and ensure a valid SR OS license file is available.


### 6. Deploy and test the example lab

```bash
cd tests
chmod +x run.sh
./run.sh deploy
```

### 7. Run all regression tests

```bash
./run.sh run --quiet --all
```

### 8. Clean up when finished

```bash
./run.sh destroy
```

---

## Coding Standards

Follow Ansible and Python best practices:

* Use the standard [Ansible module structure](https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_general.html)
* Include `DOCUMENTATION`, `EXAMPLES`, and `RETURN` blocks in every module
* Keep `galaxy.yml` metadata accurate and up to date
* Update `CHANGELOG.md` and `README.md` for user-visible changes
* Validate your work with:

  * `./run.sh sanity` or `./run.sh test`
  * Linting and style checks
  * Unit and integration test suites

---

## Commit & Pull Request Guidelines

* Write **clear, focused commits** that explain both *what* and *why*
* Reference related issues (e.g. `Fixes #42`)
* Ensure all tests pass before requesting review
* Add or update tests for new features or bug fixes
* Maintain consistent docstrings, examples, and return schemas

A pull request can be merged only when:

* All CI checks pass successfully
* A maintainer approves the change
* The update fits the project’s goals and quality standards

---

## Contributing

We welcome all contributions — from small fixes to major enhancements. Whether you’re reporting a bug, improving documentation, or extending functionality, we’d love your input.

Before submitting a pull request:

* Run all tests (`./run.sh sanity` or `./run.sh test`)
* Follow [PEP 8](https://peps.python.org/pep-0008/) and Ansible plugin guidelines
* Ensure changes are documented and clearly commented
* Update or add integration tests where relevant

---

## Getting Help

If you encounter problems or need support:

**Search existing threads**
Check [open issues](https://github.com/nokia/sros-ansible/issues) to see if your topic is already covered.

**Open a new issue**

Include the following information:

* Your **OS**, **Python**, and **Ansible** versions
* The **SR OS** and **SRLinux** versions used
* A concise problem description or error log

The maintainers and community collaborators monitor these channels and respond as time permits.