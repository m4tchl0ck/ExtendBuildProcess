# Extending the build process using the nuget package

In these days, when we are using build servers, continues integration - Jenkins, TeamCity, Azure Pipeline and so on,
we forget about such powerfull tool like MsBuild and posibility to extend build process.
In CI tools we can configure build steps, but the whole configuration stays on build server, and usualy those steps can not be reused on developers machines.
It is very good prctice to use CI tools , but sometimes some build steps should be available also on developers machines.
In these cases, msbuild comes in handy.
Decentralized build steps can bring problems when we are working with many projects/solutions, and we have to reuse build step.
In this tutorial you will see how to delivery custom build steps using nuget package.

## Build steps

In `.csproj` we are using `<Targets />` node to group tasks([read more](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild-targets)). Msbuil allows to use few types of tasks, which we can use during the build process([read more](https://docs.microsoft.com/en-us/visualstudio/msbuild/assignculture-task))

### Hello World!

Let's start with showing some message in build process. To do it we add [`<Message />` task](https://docs.microsoft.com/en-us/visualstudio/msbuild/message-task) to [`.csproj` file](ExtendBuildProcess.netframework/ExtendBuildProcess.netframework.csproj)

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    ...
    <Target Name="Custom steps" AfterTargets="Build">
        <Message Text="Hello World!" />
    </Target>
</Project>
```

Unfortunatly the result of this change cannot be seen when we build project in Visual Studio, to check if it works we have to use `msbuild.exe`(maybe you can find it in the following path `C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\MSBuild\Current\Bin\MSBuild.exe`)

![MSBuild Result](img/build-with-message.png)

### Execute external program

To check if our task is executing when we are building in Visual Studio let's change the task to create a file, in order to do it we use [`<Exec />` task](https://docs.microsoft.com/en-us/visualstudio/msbuild/exec-task) and OS instruction `echo "Hello World" >> some-file`

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    ...
    <Target Name="Custom steps" AfterTargets="Build">
        <Message Text="Hello World!" />
        <Exec Command="echo Hello World >> some-file"/>
    </Target>
</Project>
```

After `Clean` and `Build` we can find the file in the project directory

![Visual Studio Result](img/build-with-file.png)
