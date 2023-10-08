# Flutter QA

在Flutter项目开发过程中，会遇到一些问题，特此记录

## "Running Gradle task 'assembleDebug'... "

一般来说，Flutter项目调试Web都还好，但是开始实机调试的时候，我们往往会遇到一些问题，比如说

> "Running Gradle task 'assembleDebug'... "

这是因为Gradle需要下载内容，但是会一直卡住

解决方法参考如下

[flutter-app-stuck-at-running-gradle-task-assembledebug](
https://stackoverflow.com/questions/59516408/flutter-app-stuck-at-running-gradle-task-assembledebug)


1. Open your flutter Project directory.

打开flutter项目目录。

2. Change directory to android directory in your flutter project directory cd android

将目录更改为flutter项目目录中的android目录 cd android

3. clean gradle ./gradlew clean 清洁Gradle ./gradlew clean

4. Build gradle ./gradlew build or you can combine both commands with just ./gradlew clean build

构建gradle ./gradlew build ，或者您可以仅联合收割机 ./gradlew clean build 组合这两个命令

6. Now run your flutter project. If you use vscode, press F5. First time gradle running assembleDebug will take time.

现在运行您的Flutter项目。如果使用vscode，请按F5。第一次gradle运行assembleDebug将花费一些时间。

PS: Delete gradle in case of all that steps don't work

