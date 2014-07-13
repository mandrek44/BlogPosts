# Deploying to NuGet server from AppVeyor

1. Create a solution in repo with some sample class library.
2. Add package `CreateNewNuGetPackageFromProjectAfterEachBuild`:
     
        Install-Package CreateNewNuGetPackageFromProjectAfterEachBuild

3. Add `nuspec` file to project. You can use [this file](https://github.com/mandrek44/Mandro.Utils/blob/master/Mandro.Utils/Mandro.Utils.nuspec) as an example. Notice that is has a place holder for version.
4. Build your project, you should see the nupkg file create in output folder.
5. Create a GitHub repo and push the project source there.
6. Go to [AppVeyor](http://appveyor.com) and create new build project
7. Select GitHub repo (may need to link your account so AppVeyor has access). 
8. AppVeyor has added default build which will only compile sources. Go to build `Settings` and:
   - On `General` tab enable `AssemblyInfo patching`
   - On `Build` tab, set Configuration to `Release`
   - On `Artifacts` tab add artifact with path `**\*.nupkg`
   - On `Deployment` tab, add new deployment for `NuGet` provider, and fill any custom details (I use my own NuGet server)
9. Build the project - you should see the NuGet package is being created and published to NuGet server.


## Links
 - [AppVeyor](http://appveyor.com)
 - [Sample project](https://github.com/mandrek44/AppVeyorToNuGetSample)
 - [Sample nuspec](https://github.com/mandrek44/Mandro.Utils/blob/master/Mandro.Utils/Mandro.Utils.nuspec)
 - [CreateNewNuGetPackageFromProjectAfterEachBuild package](https://www.nuget.org/packages/CreateNewNuGetPackageFromProjectAfterEachBuild/)
