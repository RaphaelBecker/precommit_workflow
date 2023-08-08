# precommit_workflow

### Idea:
Inspired by: https://ljvmiranda921.github.io/notebook/2018/06/21/precommits-using-black-and-flake8/#:~:text=Before%20I%20commit%20my%20staged,necessary%20edits%20and%20commit%20again.

### 1. Initial Setup:
Ensure you have a Python project to begin with. For this example, let's create a simple "Hello World" project in bash:

`mkdir hello_world_project
cd hello_world_project
echo 'print("Hello, world!")' > hello.py`

### 2. Set Up a Virtual Environment (optional, but recommended) in bash:

`python3 -m venv venv
source venv/bin/activate  # On Windows, use: .\venv\Scripts\activate`

### 3. Install Necessary Packages:

bash:
`pip install pre-commit black flake8`

### 4. Set Up pre-commit:

Create a `.pre-commit-config.yaml` file in the root directory of your project in yaml:

```
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v3.4.0  # Use the ref you want to point at
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
    -   id: check-added-large-files

-   repo: https://github.com/ambv/black
    rev: 21.5b2  # Use the version of black you want
    hooks:
    - id: black
      language_version: python3.8  # This should match the version of python you're using

-   repo: https://github.com/pycqa/flake8
    rev: 3.9.2  # Use the version of flake8 you want
    hooks:
    -   id: flake8
```
      
### 5. Initialize pre-commit:
bash:
`re-commit install`
This command installs the pre-commit script alongside your git hooks.

### 6. Test:
Let's intentionally introduce an error in our python file hello.py:
`print(   "Hello, world!")`

Now, try to commit the changes in bash:

`git add hello.py
git commit -m "Test pre-commit"`

The pre-commit hook should kick in, and black will automatically format the code. After that, flake8 will check the formatted code against PEP8 standards.

### 7. Committing:
If black makes changes, the commit will fail (this is expected). This is because the file has been changed by black after the commit was started. You'll need to re-add the files and commit again in bash:

`git add hello.py
git commit -m "Test pre-commit"`

This time, the commit should go through without any issues, as black has already formatted the code and flake8 has verified its adherence to PEP8.

That's it! You now have an automated workflow that checks your Python code before every commit. Adjust the .pre-commit-config.yaml file as necessary to add or remove hooks based on your project's needs.
