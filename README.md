Git and Github

**Lab 1: Getting Started with Git & GitHub**

Objective: Configure Git, create repo, and push to GitHub.

Steps:
    
1. Configure Git locally:
   
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"


3. Create a folder and initialize Git:
   
mkdir git-lab && cd git-lab
git init


4. Create a file hello.txt, add, commit, and connect to GitHub:
   
echo "Hello Git" > hello.txt
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/<your-username>/git-lab.git
git push -u origin main


**Lab 2: Working with Forks and Pull Requests**

Objective: Practice contributing via fork model.

Steps:

1. Fork a public GitHub repo (e.g., octocat/Spoon-Knife).


2. Clone your fork:
   
git clone https://github.com/<your-username>/Spoon-Knife.gitcd Spoon-Knife


4. Create a branch:
   
git checkout -b feature-update


5. Add a line in index.html, commit, push:
    
git add index.html
git commit -m "Added a new line"
git push origin feature-update



6. Open a Pull Request from your fork → upstream repo.


**Lab 3: Syncing Fork with Upstream Repo**

Objective: Keep fork updated with main repo.

Steps:

1. Add upstream remote:
    
git remote add upstream https://github.com/octocat/Spoon-Knife.git
git remote -v


2. Fetch and merge upstream changes:
   
git fetch upstream
git checkout main
git merge upstream/main



3. Push updates to your fork:
    
git push origin main


**Lab 4: Branching, Rebasing & Conflict Resolution**

Objective: Learn feature branching and resolving conflicts.

Steps:

1. Create two branches:
   
git checkout -b feature1
git checkout -b feature2



2. In feature1, modify hello.txt line → commit.


3. In feature2, modify the same line → commit.


4. Merge feature2 into main, then try merging feature1 → conflict occurs.


5. Resolve conflict manually in hello.txt, mark resolved:
   
git add hello.txt
git commit



7. Try rebasing feature1 on top of main:
   
git checkout feature1
git rebase main



**Lab 4: Branching, Rebasing & Conflict Resolution**


Setup:

Create a repo git-conflict-lab.

Inside repo, create login.py:
    
def login():
    return "Login Successful"



Commit initial version:
    
git add login.py
git commit -m "Initial login function"

Steps:

1. Create 2 branches:

git checkout -b feature-frontend
git checkout main
git checkout -b feature-backend
2. Modify the same file differently in both branches:

In feature-frontend (login.py):
def login():
    return "Login via Web UI"

Commit:
git add login.py
git commit -m "Frontend: Updated login message"



In feature-backend (login.py):
def login():
    return "Login checked with database"

Commit:
git add login.py
git commit -m "Backend: Updated login with DB check"

3. Merge backend first into main:

git checkout main
git merge feature-backend

4. Now merge frontend into main → conflict!

git merge feature-frontend

Git shows:

CONFLICT (content): Merge conflict in login.py

5. Resolve conflict manually:
    
login.py now looks like:


def login():
<<<<<<< HEAD
    return "Login checked with database"
=======
    return "Login via Web UI"
>>>>>>> feature-frontend

✅ Resolve by merging both features:

def login():
    return "Login via Web UI + Database"

Mark as resolved:

git add login.py
git commit -m "Merged frontend + backend changes"

6. Try rebase (instead of merge):

git checkout feature-frontend
git rebase main

Fix conflict in same way, then:

git add login.py
git rebase --continue
