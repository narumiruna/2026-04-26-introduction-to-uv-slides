---
marp: true
theme: gaia
# header: 'My Header'
# footer: 'My Footer'
paginate: true
math: katex # or mathjax
---

<!-- _class: lead -->

# Introduction to uv

---

## Outline

- What is uv?
- Installation
- Basic usage

---

## What is uv?

An extremely fast Python package and project manager, written in Rust.

![w:1000 h:auto](https://github-production-user-asset-6210df.s3.amazonaws.com/1309177/316150505-629e59c0-9c6e-4013-9ad4-adb2bcf5080d.svg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260425%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260425T050701Z&X-Amz-Expires=300&X-Amz-Signature=b44f79033e06222648c093d9d87a8921415f5dc0c9eb192d5aad67f14c6b3e4d&X-Amz-SignedHeaders=host&response-content-type=image%2Fsvg%2Bxml)


Installing Trio's dependencies with a warm cache.


---

## [Astral](https://astral.sh/)

- Astral 是一間專注於 Python tooling 的公司
- 主要使用 Rust
- 旗下的產品有: uv, ruff, ty, pyx(beta), ...
- rye 已經不再維護了


---

## 回憶

- 先接觸 ruff
- 後來觀望 uv
- uv 支援 project management 的功能後就開始使用了
![bg right fit](https://sharex.narumi.dev/2026/04/25/xVIosHTc3bLOq6OY.png)

---

## 考古

- [2024-02-15](https://astral.sh/blog/uv): uv 為 pip, pipx, venv 的替代品
- [2024-08-20](https://astral.sh/blog/uv-unified-python-packaging): uv 加入專案管理的功能 (Cargo for Python)，可以取代 Poetry, PDM, Rye 等等
- [2025-12-16](https://astral.sh/blog/ty): ty beta release，專注於 type checking 的工具，取代 mypy, pyright 等等
- [2026-03-19](https://astral.sh/blog/openai): Astral 加入 OpenAI 的 Codex 團隊

ref: https://astral.sh/blog

---

## 印象中以前的習慣

- pip/venv + `requirements.txt` or `setup.py`
- conda + `environment.yml`
- poetry + `pyproject.toml`
- rye + `pyproject.toml`

---

## 當時為什麼改用 uv?

- 速度非常快
- 可以一次取代 pip, pipx, venv, pyenv, poetry 等等工具
- 有 cross-platform lockfile (uv.lock) 可重現度高
- 可以管理 python 版本
- 對 monorepo 支援很好 (workspace)

---

## Installation

```shell
# macOS and Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# Windows (Scoop)
scoop install main/uv
```

ref: https://docs.astral.sh/uv/getting-started/installation

---

## Upgrading uv

不會太常用到，但也不是沒機會: [uv security advisory: ZIP payload obfuscation](https://astral.sh/blog/uv-security-advisory-cve-2025-54368)

```shell
uv self update

# If you installed uv with pip, you can also upgrade it with pip:
pip install --upgrade uv
```

ref: https://docs.astral.sh/uv/getting-started/installation/#upgrading-uv

---

## Shell autocompletion

```shell
# zsh
echo 'eval "$(uv generate-shell-completion zsh)"' >> ~/.zshrc

# fish
echo 'uv generate-shell-completion fish | source' > ~/.config/fish/completions/uv.fish
```

ref: https://docs.astral.sh/uv/getting-started/installation/#shell-autocompletion

---

## Uninstallation

```shell
# Clean up stored data (optional):
uv cache clean
rm -r "$(uv python dir)"
rm -r "$(uv tool dir)"

# macOS and Linux
rm ~/.local/bin/uv ~/.local/bin/uvx
```

ref: https://docs.astral.sh/uv/getting-started/installation/#uninstallation


---

## Running script

```shell
uv run example.py

# create a Python script (optional)
uv init --script example.py --python 3.12

# Add dependencies to the script
uv add --script example.py httpx

# Run the script
uv run --script example.py
```

ref: https://docs.astral.sh/uv/guides/scripts/#running-scripts

![bg right fit](https://sharex.narumi.dev/2026/04/25/WlUxAd9v8EdgDFv4.png)

---

## Using tools

```shell
uvx ruff check

# with specific version
uvx ruff@0.3.0 check

# from github repo
uvx --from git+https://github.com/httpie/cli httpie
```

Install and run a tool
```
uv tool install ruff
ruff check
```

ref: https://docs.astral.sh/uv/guides/tools

---

## Working on projects


Create a new project:
```shell
uv init hello-world
cd hello-world
```

Initialize a project in the current directory:
```shell
mkdir hello-world
cd hello-world
uv init 
```

ref: https://docs.astral.sh/uv/guides/projects

---

## Creating a project for a library

```shell
uv init --lib

.
├── README.md
├── pyproject.toml
└── src
    └── hello_world
        ├── __init__.py
        └── py.typed

3 directories, 4 files
```

---

## pyproject.toml [(PEP 621)](https://peps.python.org/pep-0621/)

```toml
[project]
name = "hello-world"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
authors = [
    { name = "narumi", email = "toucans-cutouts0f@icloud.com" }
]
requires-python = ">=3.14"
dependencies = []

[build-system]
requires = ["uv_build>=0.9.30,<0.10.0"]
build-backend = "uv_build"
```

---

## Add packages

```shell
# Add a package to the current project
uv add httpx

# Add dev dependencies
uv add --dev ruff ty pytest pytest-cov

# Add a git dependency
uv add git+https://github.com/psf/requests
```

ref: https://docs.astral.sh/uv/guides/projects/#managing-dependencies

---

## Remove packages

```shell
# Remove a package from the current project
uv remove httpx

# Remove dev dependencies
uv remove --dev ruff ty
```

---

## References

- [Astral](https://astral.sh/)
- [Astral blog](https://astral.sh/blog)
- [uv docs](https://docs.astral.sh/uv/)