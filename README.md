# Installation

## Github package (easy way)

  1. Go to https://github.com/settings/tokens and create a new token with `read:packages`

  2. In your project root folder, create the file `github.properties` and add the following:

      ```Gradle
      gpr.usr=YOUR_USER
      gpr.key=YOUR_TOKEN  
      ```

  3. Open your `settings.gradle.kts` file and add the dependencies. Should look like:

      ```Gradle
      dependencyResolutionManagement {
          repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
          repositories {
              google()
              mavenCentral()

              val githubProperties = Properties()
              githubProperties.load(FileInputStream("./github.properties"))

              val githubPackages = listOf(
                  "https://maven.pkg.github.com/supermegazinc/Android-Escentials-Library"
              )

              githubPackages.forEach { packageUrl ->
                  maven {
                      name = "GitHubPackages"
                      url = uri(packageUrl)
                      credentials {
                          username = githubProperties["gpr.usr"] as String?
                          password = githubProperties["gpr.key"] as String?
                      }
                  }
              }
          }
      }
      ```

  4. Open your `build.gradle.kts` (app) and add the dependency:

      ```Gradle
      implementation("com.supermegazinc.libraries:escentials:VERSION")
      ```

      Change the version to the latest
  
## Manually (for coding and debugging)

  1. Download the source code
  2. Open your project root folder and create a new folder with the desired name for this library (eg. "escentials_library")
  3. Extract the code in the folder
  4. In your "settings.gradle.kts" add the following lines in the end:
      ```Gradle
      include(":escentials_library")
      ```
  5. In your build.gradle.kts (app) add the following dependencies: 
      ```Gradle
      implementation(project(":escentials_library"))
      ```