# Setup a Gradle Build Job

This page will explain to you how to setup a build job for your Maven Project.

## Creating the Job

/// note
You can skip these steps should you already have a project set up on the CI and instead directly go to [Configuration](#configuration).
///

1. Go to `https://ci.codemc.io/job/{user|organization}/newJob`
2. Enter a name for your new project and select :jenkins-freestyle-project: **Freestyle project**. Press the **OK** button at the bottom.
3. Jenkins should now create a new Job for you and redirect you to its configuration page once done.

## Configuration

We recommend to set the following settings for your project:

### :jenkins-source-code-management: Source Code Management

1. In the :jenkins-source-code-management: **Source Code Management** Section, select **Git**
2. Press **Add Repository**.
3. Enter your repository's URL in the **Repository URL** field.
4. If you only want specific branches to trigger a Build can you add a **Branch Specifier** by pressing **Add Branch**, if there isn't already one set.

### :jenkins-timer: Triggers

/// info | This is optional
You can setup automatic Builds for GitHub, GitLab, or any other supported Repository Host.  
Tutorials can be found in the [Integration Pages](../integrations/index.md) of this documenation.
///

1. In the :jenkins-timer: **Triggers** Section, check **Poll SCM**
2. Put `H/10 * * * *` in the large text field to set CodeMC to check your remote repository every 10 minutes.

### :jenkins-environment: Environment

/// info | This is optional
///

We recommend enabling **Add timestamps to the Console Output**.

### :jenkins-settings: Build

/// warning | Important
In order to build a project with JDK 8, you need to use a [workaround](../../../faq/build-jdk-8-project.md).
///

1. In the :jenkins-settings: **Build** Section, press the **Add build step** button and select **Invoke Gradle script** from the dropdown menu.
2. Press the **Use Gradle Wrapper** Radio Button.
4. Make sure **Make gradlew executable** is selected.
5. Add your tasks in the **Tasks** field. Those are usually `clean build`, `clean shadowJar` or similar.
    - You can deploy your artifacts to the CodeMC Nexus. A tutorial can be found [here](../../nexus/deploy.md).

### :jenkins-post-build: Post-build Actions

1. In the :jenkins-post-build: **Post-build Actions** Section, press the **Add post-build action** button and select **Archive the artifacts** from the dropdown menu.
2. Assuming a default build-directory, set `build/libs/*.jar` (`**/build/libs/*.jar` for multi-module projects) as the value of the **Files to archive** field.

## Final Steps

1.  Press the **Save** Button to save your changes, which will redirect you to your Project's Job page.
2.  To start a new Build, press the :jenkins-play: **Build Now** button.
3.  CodeMC will now queue a new Build to be made.  
    To see the console of your job, press the rotating icon next to the build number in the **Build** Section.