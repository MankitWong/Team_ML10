# Setup
Open a terminal (macOS/Linux) or Git Bash (Windows) in this repo, and run the following commands in order:

1. Create a virtual environment called `ml10-env`:
    ```
    uv venv ml10-env --python 3.11
    ```

2. Activate the environment:
    - for macOS/Linux:
        ```
        source ml10-env/bin/activate
        ```
        
    - for windows (git bash):    
        ```
        source ml10-env/Scripts/activate
        ```

3. Install all required packages from the [pyproject.toml](./pyproject.toml)
    ```bash
    uv sync --active
    ```

## Environment Usage
In order to run any code in this repo, you must first activate its environment.
- for macOS/Linux:
    ```
    source ml10-env/bin/activate
    ```
    
- for windows (git bash):    
    ```
    source ml10-env/Scripts/activate
    ```

When the environment is active, your terminal prompt will change to show:  
```
(ml10-env) $
```
This is your **visual cue** that you’re working inside the right environment.  

When you’re finished, you can deactivate it with:  
```bash
deactivate
```
