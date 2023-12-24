# DOCUMENTING MY LAB STEPS

This document contains all the steps followed to setup the documentation for this and future projects. I took time to document the steps for installing setupa and using the following: 

1. **Github Account**
2. **VSCode**
3. **Git Bash**
4. **Markdown**

## Github: 

### Step 1:
I already had a github account set up so i logged in as shown:

![Enter Username and password](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/github_login.jpg)

### step 2:

I created a new repository by clicking on ``new``   and naming the repo AWS

![New Repo](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/new_repo.jpg)

### Step 3:

From VSCode, click ``file`` and select ``open folder``. choose the folder to  which the repository will be cloned to.

### Step 4: 

Go to github and click on the new repo created, Click on ``code``, copy the htpps code

### Step 5:

Go to VSCode and click on right click on the folder into which you want to clone the new repo into and click ``open in integrated terminal``

### Step 6:

In the terminal, type ``git init`` to initialize git in the folder, type ``git clone`` and then paste the code link that was copied in **Step 4** above 

### Step 7

in the terminal type ``touch`` and the name of the file you want to create **Exmaple: touch assignment.md**

After editing the document and adding all the necessary files, save it. 

### Step 8 
type ``git add .``

type  ``git commit -m`` and  "add a commit message"

### Step 9

type ``git push`` 

at this point you will be asked for your user name: enter you username

Next you will be prompted for you password: the password is you personal Access Token (PAT). Steps to create a PAT are covered in the Next Session.


## HOW TO GENERATE YOU PERSONAL ACCESS TOKEN

1. ``login`` to your github profile:

![github login page](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/github_login.jpg)


2. Go to ``settings`` and click ``developer settings``

![developer setings](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/Developer%20Settings.JPG)


3. Click on ``Personal access tokens`` and choose ``classic tokens``

![personal Access Tokens](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/Classic_tokens.JPG)


4. Click ``Generate Token`` select the classic tokens option
![Choose Generate Token](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/generate_token.JPG)


5. Give a descriptive name to the token in the note textbox provided


6. choose how long you want the token to last (Expiration date)


![Further settings](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/final_steps.JPG)

choose the scope od the access for the token. Usually, choosing **Repo** would do


7. click ``generate token``

![Final step](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/generate_token_final.JPG)


8. Copy out the token to somewhere safe.


## VSCODE:

Vscode was installed but to achieve this assignment, i had to do the following
 
  - Update my vscode
  - connect vscode to my github account
  - Install markdown Extension

 
 ## STEPS TO UPDATE VSCODE:

 1. On the lower left corner of vscode, click :gear: 
 2. Click on ``update and restart``
 
 **vscode** updates and restarts the application automatically




### STEPS TO CONNECT VSCODE TO GITHUB

1. Click on accounts :man: icon by th lower left conner of vscode
2. select 11sign in to sync setting``

![Sign in to synch settings](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/vs_code_signin_to_sync.jpg)

3. it redirects to the default browser for sign in.
4. Enter you github username and password and enter
5. A request for authorization page shows up click on ``authorize visual-studio-code``

![Authorize Vscode](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/Request_for_authorization.JPG)

Done! 


## INSTALLING MARKDOWN EXTENSION
1. Click on Extension icon 
2. In the search tab, type ``markdown``
3. 3. choose ``github markdown preview``


![Github markdown preview](/AWS/aws-educate-labs/assets/screenshots/001-assignment_on_markdown/Github_Markdown_Preview.JPG)

4. click on ``install``
5. click on file, new file
6. rename the file with the ``.md`` eg **README.md** 

Done! Enjoy.


## GITBASH

Git bash was installed already.