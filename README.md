# STEP BY STEP
## 1. Set Up
## - Installing Java 11
## - Installing IntelliJ
## - Installing Chrome Browser
## - Installing Chrome Driver
 ## - Creating a New Project
- We want to create a Maven project.
-  In here, they're going to ask you for a GroupId and an ArtifactId.
- Next it will ask you the location of where you want to store the project.
- Now there are a couple of things we want to add into here — the first thing we want to add is the properties.

`<properties>
    <maven.compiler.target>1.12</maven.compiler.target>
    <maven.compiler.source>1.12</maven.compiler.source>
</properties>`
***note**: en Intellij 2023 version properties are added by default.*
- The next thing we want to do is to add dependencies because we're using Selenium WebDriver.
- Okay, let's paste this under the properties and we notice that we get a little error.
That's because this needs to be in dependency section.
- Create new resources directory 
