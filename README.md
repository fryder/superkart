# SuperKart — Sales Forecasting Notebook

Short guide to set up the development environment and resolve a common XGBoost issue on macOS.

## Quick setup (macOS / Linux / WSL)

1. Create and activate a virtual environment in the project root:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Upgrade packaging tools and install requirements:

```bash
".venv/bin/python" -m pip install --upgrade pip setuptools wheel
".venv/bin/python" -m pip install -r requirements.txt
```

3. (Optional) If you prefer to install directly from the notebook, run the install cell which uses the notebook's Python interpreter.

## macOS — Fix for XGBoostError (missing OpenMP / `libomp`)

If you see an error like `XGBoostError: Library not loaded: @rpath/libomp.dylib` or the notebook traceback mentions `libxgboost.dylib` / `libomp.dylib`, install Apple Homebrew's OpenMP runtime and then reinstall `xgboost` into your environment:

```bash
# Install libomp (Homebrew)
brew install libomp

# Reinstall xgboost into the same Python environment used by your notebook
".venv/bin/python" -m pip uninstall -y xgboost
".venv/bin/python" -m pip install xgboost
```

Notes:
- Replace `".venv/bin/python"` with the path to the Python interpreter you use if different (for example, a named virtualenv or conda env).
- After installing `libomp` you may need to restart your terminal, IDE, or Jupyter kernel so the library path is picked up.

## Notebook

- Notebook: `Full_Code_SuperKart_Model_Deployment_Notebook_[Updated].ipynb`.
- The installation cell has been updated to use the notebook's Python interpreter so installs go to the correct environment.

## Troubleshooting

- If `xgboost` still fails after installing `libomp` and reinstalling, ensure you are using a 64-bit Python and that the `xgboost` wheel matches your platform. Consider creating a fresh venv and re-installing.
- If you want, I can pin package versions in `requirements.txt` by running pip installs and producing a `pip freeze` output.

## Contact

If you want, I can also add a short troubleshooting cell in the notebook (already added) and commit it — tell me if you'd like me to push these changes to the remote.
