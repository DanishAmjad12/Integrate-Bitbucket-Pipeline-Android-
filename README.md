# Integrate-Bitbucket-Pipeline-Android

Bitbucket pipeline is an Integrated service built on Bitbucket Cloud where we can automatically test, build, and deploy the code based on the configuration file.

# Prerequisites
* You need to create a Bitbucket cloud account
* You should have one repository in that account.

# Step 1: Enable Pipeline
The first step is to enable Pipeline in your Bitbucket repository settings.

* Go To Bitbucket Project
* Repository Setting
* Pipeline Section — > Settings
* Enable Pipeline ✅

# Step 2: Create Pipeline

Step 2 is to create a pipeline to generate a YAML file and added to your Android Project.

* Go to your repository and select Pipelines.
* Click Create your first pipeline and Select the template that is Recommended or you can choose another as well.
* After selecting the template you will see the Editor of the YAML file with the name bitbucket-pipeline.yml
* Commit and run

# Step 3: Basic Configuration
After making a file, let’s add some basic configuration to build an Android application. For instance, when we upload code to a particular branch, we want it to create a debug build.

Now let’s jump into the file to see how the file looks in practice:

```
image: androidsdk/android-30
pipelines:
  branches:
      staging:               # pipeline definition for all branches
        - step:              # step to build Android debug application
            name: Android Staging Build Generating..
            size: 2x        # Double resources available for this step.
            caches:        # caching speed up subsequent execution https://support.atlassian.com/bitbucket-cloud/docs/cache-dependencies/
              - gradle
            script:
              - chmod +x gradlew
              - ./gradlew assembleDebug
            artifacts:
              - app/build/outputs/**        # artifacts are files that are produced by a step https://support.atlassian.com/bitbucket-cloud/docs/use-artifacts-in-steps/
```

The configuration has a pipeline definition for all branches, with one step: running the command ‘./gradlew assembleDebug’. Once you push code to the staging branch, you can check the Pipeline status, view detailed logs, and access other useful data.

Here we also added a cache to make Android builds faster It enables caches on external libraries and directories such as Gradle libraries, to enable the cache just added this command.

```
caches:    # caching speed up subsequent execution https://support.atlassian.com/bitbucket-cloud/docs/cache-dependencies/
- gradle
```

# Step4: Build and Test
The ultimate step is to build and test the pipeline. Once it’s finished, you can grab the built .apk file in the artifacts directory.

* Go to artifacts
* app/builds/outputs/debug.apk
* Download the file

If you want a bundle release build then just add this command in the bitbucket-pipeline.yml file.

```
      releaseStore:
        - step:
            name: Android Prod Build App Bundle Generating..
            size: 2x
            caches:
              - gradle
            script:
              - chmod +x gradlew
              - ./gradlew bundleRelease
            artifacts:
              - app/build/outputs/**

```

If you want to explore more about Bitbucket Pipeline, then check out these sources: ➡️ [Link](https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/?source=post_page-----01171ddd324e--------------------------------)

```
Thanks, If you think something is missing, have questions, or would like to offer any thoughts or suggestions, do share. and if you want to contribute, please do 😊 and follow me here👇
 ```
 * Twitter (https://twitter.com/DanishAmjad10)
 * Medium (https://medium.com/@DaniAmjad)
 * LinkedIn (https://www.linkedin.com/in/danish-amjad-06a43090/)
 * YouTube (https://www.youtube.com/channel/UC06GphxCS1gzZhdT9dn6kQA?view_as=subscriber)

