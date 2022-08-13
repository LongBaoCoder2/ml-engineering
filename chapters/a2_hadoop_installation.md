# Install Hadoop
- Install Java JDK: `brew install --cask homebrew/cask-versions/adoptopenjdk8`
  - Check Java version: `java -version`
  - Confirm you have the correct version of java (version 8) on your machine. If it returns anything other than `1.8.*`, be sure to install the correct version.
  - Find Java Home path: `/usr/libexec/java_home` &#8594; `/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home`
- Install Hadoop: `brew install hadoop`
# Hadoop Environment Variable Settings
- The document containing the environment variable settings locates at `/usr/local/Cellar/hadoop/3.3.4/libexec/etc/hadoop`
- Add Java Home path into `hadoop-env.sh`: 
```sh
# hadoop-env.sh

# The java implementation to use. By default, this environment
# variable is REQUIRED on ALL platforms except OS X!
export JAVA_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
```
