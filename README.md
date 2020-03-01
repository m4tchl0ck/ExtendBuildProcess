# Extending the build process using the nuget package

In these days, when we are using build servers, continues integration - Jenkins, TeamCity, Azure Pipeline and so on,
we forget about such powerfull tool like MsBuild and posibility to extend build process.
In CI tools we can configure build steps, but the whole configuration stays on build server, and usualy those steps can not be reused on developers machines.
It is very good prctice to use CI tools , but sometimes some build steps should be available also on developers machines.
In these cases, msbuild comes in handy.
Decentralized build steps can bring problems when we are working with many projects/solutions, and we have to reuse build step.
In this tutorial you will see how to delivery custom build steps using nuget package.
