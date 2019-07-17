# BlankXamarinFormsAppFromSource

Builds steps currenty used to build dlls:
1. `cd Xamarin.Forms/`
2. `open Xamarin.Forms.sln`
3. Wait for nuget packages to be restored.
4. `msbuild Xamarin.Forms.Build.Tasks/Xamarin.Forms.Build.Tasks.csproj`
5. `msbuild /restore /p:Platform=iPhoneSimulator Xamarin.Forms.sln`

Build steps currenlty used to build blank app:
1. `cd BlankXamarinFormsApp/`
2. `open BlankXamarinFormsApp.sln`
3. Right mouse click the Forms project (BlankXamarinFormsApp) and build.

Current issues: 
- Attempting to build BlankXamarinFormsApp results in 4 errors.
```
BlankXamarinFormsAppFromSource/BlankXamarinFormsApp/BlankXamarinFormsApp/App.xaml: Error: The target "UpdateDesignTimeXaml" does not exist in the project. (BlankXamarinFormsApp)

BlankXamarinFormsAppFromSource/BlankXamarinFormsApp/BlankXamarinFormsApp/MainPage.xaml: Error: The target "UpdateDesignTimeXaml" does not exist in the project. (BlankXamarinFormsApp)

BlankXamarinFormsAppFromSource/BlankXamarinFormsApp/BlankXamarinFormsApp/MainPage.xaml.cs(13,13): Error CS0103: The name 'InitializeComponent' does not exist in the current context (CS0103) (BlankXamarinFormsApp)

BlankXamarinFormsAppFromSource/BlankXamarinFormsApp/BlankXamarinFormsApp/App.xaml.cs(13,13): Error CS0103: The name 'InitializeComponent' does not exist in the current context (CS0103) (BlankXamarinFormsApp)
```