# BlankXamarinFormsAppFromSource

This repo contains two sample projects which show how to build Xamarin.Forms (v4.1) from source. One project uses pre-built dlls, the other includes the csproj files and references the project directly.

All of these steps were created for building on macOS and deploying to an iPhone simulator. To build on Windows the steps may vary. See known issues below.

## Building the BlankXFAppFromDll project

1. From termianl navigate to the Xamarin.Forms submodule

    `cd Xamarin.Forms/`

2. Open the solution in Visual Studio.
    
    `open Xamarin.Forms.sln`

3. Wait for the nuget packages to be restored, then close Visual Studio.
4. Build the build tasks.
    
    `msbuild Xamarin.Forms.Build.Tasks/Xamarin.Forms.Build.Tasks.csproj`

5. Build Xamarin.Forms solution for specific platoform, in thise case iPhoneSimulator

    `msbuild /restore /p:Platform=iPhoneSimulator Xamarin.Forms.sln`

    Note: It may not be required to specifiy platform on Windows. 

6. Now navigate to the BlankXFAppFromDll directory and open BlankXFAppFromDll.sln

    `open ../BlankXFAppFromDll/BlankXFAppFromDll.sln`

7. You should now have no issues building the BlankXFAppFromDll and BlankXFAppFromDll.iOS projects.

## Building the BlankXFAppFromCSProj project

1. Open BlankXFAppFromCSProj.sln in the BlankXFAppFromCSProj directory.
2. Wait for nuget packages to restore. 
3. One by one go through and build each of the projects in the Xamarin.Forms solution folder. The order of what project you build when may matter. But keep going through and building what it errors on and you should get there.
4. You should now have no issues building the BlankXFAppFromCSProj and BlankXFAppFromCSProj.iOS projects.


## The secret sauce to add Xamarin.Forms to your own project

This repo came around becase of [this issue](https://github.com/xamarin/Xamarin.Forms/issues/6884) filed on the Xamarin.Forms repository. The main things I was missing was adding the props/targets for building xaml files. Helping resolve that issue came from [this](https://github.com/xamarin/Xamarin.Forms/issues/6884#issuecomment-512122234) comment.

Open your Xamarin.Forms csproj file in your favourite editor and add the following lines (updating the path to your Xamarin.Forms source)

```
<Import Project="..\..\Xamarin.Forms\.nuspec\Xamarin.Forms.DefaultItems.props" />
<Import Project="..\..\Xamarin.Forms\.nuspec\Xamarin.Forms.DefaultItems.targets" />
<Import Project="..\..\Xamarin.Forms\.nuspec\Xamarin.Forms.targets" Condition="'$(BuildingInsideVisualStudio)' == 'true'" />
<Import Project="..\..\Xamarin.Forms\.nuspec\Xamarin.Forms.targets" Condition="'$(BuildingInsideVisualStudio)' != 'true'" />
```

## Known Issues:
- All these build steps were done on macOS. It's unknown if these same steps work on Windows.
- Android project is not supported currently.
- Xamarin.Forms test projects are .NET Standard. It's unknown if shared or PCL projects will function correctly.
- Not all features are added/tested (eg. Maps)
- The dll/csproj references are not the bare minimum required to get the project to run. You may be able to remove some of these references and have the project work correclty. This repo was put into a functional state and commited.