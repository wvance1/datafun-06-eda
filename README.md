# datafun-06-EDA

### Project 6 will be a creation of my own. I will be demonstrating the topics coverd so far in the course on a data set of my choosing.

## creating project and cloning to machine

##### I creatred a new repository on GitHub. 
##### I made sure that the README.md was checked so that I could write this little note!
##### I then went to a folder on my computer, where I wanted to file to live, and I opened the terminal for that file.
##### I then cloned the repository to that folder using the following command:
```shell

git clone site_URL

```

## Adding files 

##### I then added a .py file to work in, requirements.txt to hold the required project modules, a .vinv to act as the virtual environment(instructions for that are below), and a .gitignore to hold the .venv and the .vsode file so that the virtual environment is not passed to the rest of the python environment.

## Create Project Virtual Environment

##### On Windows, create a project virtual environment in the .venv folder. 

```shell
#creates .venv file then activates it
py -m venv .venv
.venv\Scripts\Activate

```

## Install all required packages into local project virtual environment

##### This installs the required packages that are held in the requirements.txt file - requests 

```shell

#installs all files in requirements.txt
py -m pip install -r requirements.txt
#creates requirements.txt file and outputs the installed packages
py -m pip freeze > requirements.txt
```

## add docstring to .py file

##### Added a note to the top of the file bound by '''note'''

## Git add and commit 

##### Periodically, I will add, commit and push the file to the web. 

```shell
git add .
git commit -m "add .gitignore, cmds to readme"
git push origin main
```
## Selected Data set

##### I wll be looking at the titanic data set from seaborn. It is a built in data set, so no other imports were needed. I displayed the head to help observe the data.

```shell
# Load the Titanic dataset
titanic_df = sns.load_dataset('titanic')

# Display the first few rows of the dataset
print(titanic_df.head())

#Downloaded the data set to a CSV
titanic_df.to_csv('titanic_dataset.csv', index=False)

```

## Source
##### This project was built to the following specification:
- [datafun-06-eda](https://github.com/denisecase/datafun-06-spec)