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
  
The extra 0 from 00 - 09 keeps the folders in numerical order when executing the list ls command. The you in 6 months or the next person on the project will thank you as it is easy to numerically follow the steps based on the folder number and the date the folder was generated ls -lha.

The name of your project folder should be descriptive of the project, for example, WhiteAbaloneRNA-Seq or SeriolaGWAS.
