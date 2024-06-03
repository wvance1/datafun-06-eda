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

### We will look at information pertaining to the death rates by gender and class.
##### Graph of age distribution
```shell
# Bar graph of the age distribution
plt.figure(figsize=(6, 4))
sns.histplot(titanic_df['age'].dropna(), bins=30, kde=False)
plt.title('Age Distribution')
plt.xlabel('Age')
plt.ylabel('Count')
plt.show()
print(f'Average Age: {titanic_df.age.mean():.2f}')
print(f'Q1: {titanic_df.age.quantile(.25)}')
print(f'Q3: {titanic_df.age.quantile(.75)}')

```
##### Graph of gender distribution
```shell
# Bar graph of the gender distribution
plt.figure(figsize=(2, 3))
ax = sns.countplot(data=titanic_df, x='sex')
plt.title('Gender Distribution')
plt.xlabel('Gender')
plt.ylabel('Count')

# Adding values on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), 
                (p.get_x() + p.get_width() / 2., p.get_height()/2), 
                ha = 'center', va = 'center', 
                xytext = (0, 0), 
                textcoords = 'offset points')

# Assigns bar colors
colors = ['lightblue', 'hotpink']
for bar, color in zip(ax.patches, colors):
    bar.set_color(color)

plt.show()
print(f'Percent male: {round((577/(577+314)*100))}%')
print(f'Percent female: {round((314/(577+314))*100)}%')

```
##### Graph of survivors by gender
```shell
# Bar graph of survivors by gender
plt.figure(figsize=(4, 4))
ax = sns.countplot(data=titanic_df, x='sex', hue='survived')
plt.title('Survival by Gender')
plt.xlabel('Gender')
plt.ylabel('Count')
plt.legend(title='Survived', labels=['No', 'Yes'])

# Adding values on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), 
                (p.get_x() + p.get_width() / 2., p.get_height()/2), 
                ha = 'center', va = 'center', 
                xytext = (0, 0), 
                textcoords = 'offset points')

# Assigns bar colors
colors = ['red', 'red','lightblue', 'hotpink']
for bar, color in zip(ax.patches, colors):
    bar.set_color(color)

# Change legend colors
colors = ['lightblue', 'hotpink', 'red']
legend_labels = ['Male Survived', 'Female Survived', 'Died']
handles = [plt.Line2D([0], [0], marker='o', color='w', markerfacecolor=color, markersize=10) for color in colors]
ax.legend(handles, legend_labels, title='Gender')

plt.show()

print(f'Percent male Death: {round((468/(577)*100))}%')
print(f'Percent female Death: {round((81/(314))*100)}%')
```
##### Graph of survivors by class
```shell
# Bar graph of class vs. survival
plt.figure(figsize=(6, 4))
ax = sns.countplot(data=titanic_df, x='class', hue='survived')
plt.title('Survival by Passenger Class')
plt.xlabel('Class')
plt.ylabel('Count')

# Adding values on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), 
                (p.get_x() + p.get_width() / 2., p.get_height()/2), 
                ha='center', va='center', 
                xytext=(0, 0), 
                textcoords='offset points')

# Customize legend
colors = ['red', 'gold', 'silver', 'brown']
legend_labels =['died', 'Survived 1st-class', 'Survived 2nd-class','Survived 3rd-class']
handles = [plt.Line2D([0], [0], marker='o', color='w', markerfacecolor=color, markersize=10) for color in colors]
ax.legend(handles, legend_labels, title='Survival')

# Assigns bar colors
colors = ['red', 'red', 'red', 'gold', 'silver', 'brown']
for bar, color in zip(ax.patches, colors):
    bar.set_color(color)

plt.show()

print(f'Percent Death 1st class: {round((80/(80+136)*100))}%')
print(f'Percent Death 2nd class: {round((97/(97+87))*100)}%')
print(f'Percent Death 3rd class: {round((372/(372+119))*100)}%')
```
##### Graph of survivors by class and gender
```shell
# Create a FacetGrid for the different classes
g = sns.FacetGrid(titanic_df, col='class', height=4, aspect=1.2)

# Create the bar plot on each facet
g.map_dataframe(sns.countplot, x='sex', hue='survived', palette='Set1')

# Add titles and labels
g.set_axis_labels("Sex", "Count")
g.add_legend(title='Deaths by Gender and Class', label_order=['died', 'survived'],labelcolor=['red', 'blue'])
g.set_titles(col_template="{col_name} Class")

# Add counts and percentages on the bars
for ax in g.axes.flat:
    for p in ax.patches:
        count = p.get_height()
        total = len(titanic_df[(titanic_df['class'] == ax.get_title().split()[0]) & (titanic_df['sex'] == p.get_x())])
        ax.annotate(f'{count}',
                    (p.get_x() + p.get_width() / 2., p.get_height()), 
                    ha='center', va='center', 
                    xytext=(0, 5), 
                    textcoords='offset points')

plt.show()

print(f'Percent Death 1st class Male: {round((3/(94)*100))}%')
print(f'Percent Death 1st class Female: {round((77/(122)*100))}%')
print(f'Percent Death 2nd class Male: {round((6/(76))*100)}%')
print(f'Percent Death 2nd class Female: {round((91/(108))*100)}%')
print(f'Percent Death 3rd class Male: {round((300/(347))*100)}%')
print(f'Percent Death 3rd class Female: {round((72/(144))*100)}%')
```
##### Box plot of survival and ticket price
```shell
# Create the box plot
plt.figure(figsize=(5, 6))
sns.boxplot(data=titanic_df, x='survived', y='fare', showfliers=False, palette={0: 'red', 1: 'blue'})

# Add titles and labels
plt.title('Ticket Price vs. Survival Status')
plt.xlabel('Survived')
plt.ylabel('Ticket Price')
plt.xticks([0, 1], ['Died', 'Survived'])

plt.show()

```

##### The data can be found at the below link.
[Titanic Data](https://github.com/wvance1/datafun-06-eda/blob/main/titanic.csv)

## Source
##### This project was built to the following specification:
- [datafun-06-eda](https://github.com/denisecase/datafun-06-spec)