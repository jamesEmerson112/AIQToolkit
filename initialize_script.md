# AIQToolkit Setup Guide (initialize_script.md)

This guide documents the step-by-step process to set up the AIQToolkit development environment on Windows, starting from fetching LFS data to a working CLI. Follow these instructions for a smooth setup in the future.

---

## 1. Fetch LFS Data

```bash
git lfs install
git lfs fetch
git lfs pull
```

---

## 2. Create and Activate the Virtual Environment

**Create venv (using uv):**
```bash
uv venv --seed .venv --python 3.12
```

**Activate venv:**

- **Git Bash:**
  ```bash
  source .venv/Scripts/activate
  ```
- **Command Prompt:**
  ```
  .venv\Scripts\activate
  ```
- **PowerShell:**
  ```
  .venv\Scripts\Activate.ps1
  ```

Your prompt should now start with `(.venv)`.

---

## 3. Install Python Dependencies

**Full install (recommended for development):**
```bash
uv sync --all-groups --all-extras
```

---

## 4. Install AIQToolkit in Editable Mode

```bash
uv pip install -e .
```

---

## 5. Verify the CLI

```bash
aiq --version
```
You should see output like:  
`aiq, version 1.1.0rc5.devXX+gXXXXXXX`

If you see a "not recognized" error, make sure your venv is activated and repeat step 4.

---

## 6. Troubleshooting

- **Build errors for C/C++ extensions:**  
  Install Microsoft C++ Build Tools (see Prerequisites).
- **venv activation issues:**  
  Use the correct command for your shell (see step 2).
- **CLI not found:**  
  Ensure venv is activated and run `uv pip install -e .` again.

---

## 7. Next Steps

- Explore examples in the `examples/` directory.
- See the main [README.md](README.md) for usage and documentation.

---

**This guide ensures a repeatable, reliable setup for AIQToolkit development on Windows.**
