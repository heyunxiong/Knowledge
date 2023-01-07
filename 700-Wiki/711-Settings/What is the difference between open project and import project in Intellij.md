# What is the difference between open project and import project in Intellij?
https://stackoverflow.com/questions/37304297/what-is-the-difference-between-open-project-and-import-project-in-intellij
---
When first starting up Intellij IDEA you are given some quick start options which include Import Project and Open Project. What is the difference between these two options?

According to the answer in [Difference between open and import a project in androidstudio](https://stackoverflow.com/questions/32353900/difference-between-open-and-import-a-project-in-androidstudio) open is used for existing projects and import is for migrating from other environments. However when testing, I am able to open both [existing projects already in Intellij and projects from other IDEs] using either Import or Open project.

I am wondering if the meaning is different for Intellij vs Android Studio.

Note: I have never used Android Studio so please excuse me if it shows the same behavior.

---

Basically you can use Open every time as it works both for new and existing projects.

The only additional feature of Import is that you can set new project name and location if you wish to and additionaly do some basic config stuff such as Add Framework support (but thiis you can do even if you open project later). My personal preference is to use only Open as Import is rarely necessary for me.


---
At least for IDEA 2018.1 and 2018.2, there're extra differences when working with Gradle projects:

1.  .idea/libraries/*.xml and .idea/modules.xml are only generated in case the project was opened. They're not in case it was imported.
    
2.  The generated .iml files are slightly different (the imported version doesn't list any libraries, so I assume IDEA relies on the underlying foreign project model for imported projects).
    

Since it works both ways, I prefer importing projects as it results in less IDEA-specific generated files.