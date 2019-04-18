## 生物信息项目管理  

### 几个基本原则  
* Reproducibility (version, hash, date of download)  
* Version Control  
* Extensive commentary  

Project management is defined as the process of keeping track of the many inputs and outputs of a project from experimental design through publication.

Many components of a project are generated, in an attempt to organize the inputs and outputs of a project. How these components relate to each other and their organized is directly related to project management.

The main components of project management include but may not be limited to:

1. Folders and Files  
2. Notebook record of commands, thought process and related code  
3. Communication and Discussion  
4. ToDo list  
5. Record of your time spent  

The rest of this tutorial steps through the components of project management, how they are related and importantly how the adoption of some very simple rules help integrate these components and do not come with a large learning curve that can be prohibitive to quick adoption by your team.  

### 1. Folders and Files  
Most people use folders to organize their files regardless of operating system (Windows, IOS, Linux). A small change to how folders are labeled can significantly improve the ability for others to follow what you did, the order you did it in and where you did it.

Number folders in order of their creation

Prepend the descriptive folder name that you usually create with a number starting with 00, followed by 01, 02, 03 and so forth like so:

* Project folder
  * 00_RawData
  * 01_AnalysisStepOne
  * 02_AnalysisStepTwo
  * 03_AnalysisStepThree
  
The extra 0 from 00 - 09 keeps the folders in numerical order when executing the list `ls` command. Then you in 6 months or the next person on the project will thank you as it is easy to numerically follow the steps based on the folder number and the date the folder was generated `ls -lha`.

The name of your project folder should be descriptive of the project, for example, WhiteAbaloneRNA-Seq or SeriolaGWAS.

### 2. Notebook  
Science isn’t reproducible if it isn’t recorded. Traditionally, paper notebooks have been used in the wet lab to record the science performed that day and the outcome. In bioinformatics, science is recorded digitally in a digital notebook. We recommend using GitHub as your digital notebook.

#### GitHub  
GitHub is often thought of as a tool for programmers to version control code but it can also be used to version control text documents as an online notebook. If you don’t have a GitHub account, you can set one up based on this GitHub Tutorial and the free version of GitHub now allows for unlimited free repositories. In addition, as a researcher or educator you can request a free upgrade to get access to unlimited users in private repos..

One of the great aspects of GitHub is that you can use markdown syntax to very quickly format your notebook. For example, This tutorial is written in markdown and you can make headers# ## ###, bullet points *, code blocks and insert images very easily. Markdown can also be easily converted to PDF for sharing.

Assuming you now have a GitHub account, create a GitHub repository with the same name you labeled your project folder (ie: WhiteAbaloneRNA-Seq or SeriolaGWAS).

Here is the first integration between project components.

#### For every subfolder create a markdown file

For every subfolder you make in your project folder on your remote machine or computer, create a markdown file in your GitHub repository.

* Notebook_LastName
 * 00_RawData.md
 * 01_AnalysisStepOne.md
 * 02_AnalysisStepTwo.md
 * 03_AnalysisStepThree.md
After you git clone your repo you can create a folder named Notebook_LastName and then add markdown files corresponding to each new subfolder you add during the analysis pipeline.

If you work on multiple machines and your laptop then create a folder for each machine.

* Notebook_LastName
 * remote machine
  * 00_RawData.md
  * 01_AnalysisStepOne.md
  * 02_AnalysisStepTwo.md
  * 03_AnalysisStepThree.md
 * laptop
  * 01_AnalysisStepOne.md
  * 02_AnalysisStepTwo.md
  
#### Atom (text editor)
If you haven’t already, download and install GitHub ATOM. This is a text editor that understands markdown syntax and allows you to preview markdown that you write in an adjacent window. See markdown tutorial for more information.

What, When, Where, Why, How and the Result
For every step you perform bioinformatically, record it in your markdown file along with

Title
Date
Computername and path of working directory
Description of what you are trying to do and why
Code block of the commands you used
Description of the result
This last step is important as it is a discrete block of notes that is the smallest unit of replicable notes in your notebook. The Why, How and Result can be replicated multiple times if it is the same day in the same folder.
