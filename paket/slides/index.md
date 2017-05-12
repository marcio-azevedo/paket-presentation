- title : Dependency Management done right!
- description : Introduction to PAKET
- author : Márcio Azevedo
- theme : night
- transition : default

***

## Dependency Management done right!

<br />
<br />

### Introduction to PAKET!

<br />
<br />

[Márcio Azevedo](https://github.com/marcio-azevedo/presentations/)

***

Back in the old days...

' there was the ~\Libs\ folder

![Lib folder](images/lib-folder.png)

...and when NuGet showed up, it made referencing a breeze.

--- 

But then, there was a new problem...
' instead of DLL Hell, there was

<img src="images/nuget-hell.png" style="background: transparent; border-style: none;" width=450 />

' Note: NuGet (the command tool) works well for simple, small projects, not for complex and large ones!

---

### So, what's the solution!?

![funny pic](images/RequestForComment.gif)
<!--![funny pic](images/solution.gif)-->

***

### PAKET
#### Dependency Manager for .NET (and Mono)
![PAKET](images/paket-logo.png)

> **designed to work well with NuGet packages** and also
> enables referencing files directly from Git repositories or any HTTP resource.
' Why PAKET?
' PAKET offers **predictable control** over references with NuGet!
> It enables **precise and predictable control** over what packages the projects within your application reference.

---

' Here's some problems with NuGet command tool
### NuGet (the command tool) has no concept of transitive dependencies

<img src="images/masstransit-dependencies.png" style="background: transparent; border-style: none;" width=300 />
<img src="images/package.config.png" style="background: transparent; border-style: none;" width=300 />

---

### NuGet puts the package version in the path

<img src="images/package-version-in-path.png" style="background: transparent; border-style: none;" width=450 />
<img src="images/package-version-in-path1.png" style="background: transparent; border-style: none;" width=450 />

' Problems: path to packages changes at every update, code reviews are harder because you're always updating .csproj files, etc

---

### Updates may require manual work (specially if you update framework)

![NuGet](images/csproj-references.png)

How PAKET does it:

![PAKET](images/csproj-paket-references.png)

' Neither Visual Studio neither NuGet are clever to update it when you change the project Framework.

***

### paket.bootstrapper.exe

* Don't need to commit paket.exe to your repository
* Bootstrapper is available for download - [Bootstrapper](https://github.com/fsprojects/Paket/releases/latest)
* Bootstrapper allows to download latest paket.exe
* Can be used for CI build or from inside Visual Studio

![Bootstrapper](images/paket.bootstrapper.exe.png)

' Main components
' http://fsprojects.github.io/Paket/paket-simplify.html#Sample

---

### Paket.exe (~/.paket directory in root)

```sh
$ .paket\paket.exe --help
```

<img src="images/paket-cmds.png" style="background: transparent; border-style: none;" width=600 />

' Bootstrapping - Don't commit paket.exe to your repository
' Bootstrapper is available for download - https://github.com/fsprojects/Paket/releases/latest
' Bootstrapper allows to download latest paket.exe
' Can be used for CI build or from inside Visual Studio

---

' Show convertion from NuGet

http://fsprojects.github.io/Paket/paket-convert-from-nuget.html
https://gist.github.com/marcio-azevedo/9576969640a404fd2944aab89117d212

---

### Global definition of dependencies
**paket.dependencies** (in solution root)

    source https://dotnet.myget.org/F/dotnet-core/api/v3/index.json

    // Reference a nuget package
    nuget FSharp.Management
    // Reference a single file from GitHub
    github myRepo/aProject dependency.dll 

    // Shared dependencies
    nuget Newtonsoft.Json
    nuget FSharp.Core

    group Web
        nuget Fake.IIS
        nuget Suave

    group Database
        nuget FluentMigrator
        nuget SQLProvider

---

### List of used versions for all dependencies
**paket.lock** (generated from paket install)

    NUGET
      remote: https://api.nuget.org/v3/index.json
        Microsoft.Bcl (1.1.9) - framework: >= net45
          Microsoft.Bcl.Build (>= 1.0.14)
        Microsoft.Bcl.Build (1.0.21) - import_targets: false, framework: >= net45
        Microsoft.Net.Http (2.2.28) - framework: >= net45
          Microsoft.Bcl (>= 1.1.9)
          Microsoft.Bcl.Build (>= 1.0.14)
        NuGet.CommandLine (3.5)

---

### Dependency definition per project ("replaces" packages.config)
**paket.references** (in each project folder)

    Microsoft.Net.Http
    Newtonsoft.Json

---

### Package definition for new packages
**paket.template**

***

asdf

***

![PAKET](images/paket-logo.png)

### Some References

* [ElasticSearch.NET](https://github.com/elastic/elasticsearch-net) uses this in their .NET tools and libraries
* [Jet.com](https://github.com/jet/kafunk) (e-commerce platform recently acquired by Walmart by 3bn $)

---

![PAKET](images/demo.jpeg)

---

### RECAP

* Plain text over Command line tool
* Direct vs. transitive dependencies
* Only one version of a package

There's also a VS extension - [Paket.VisualStudio](https://github.com/hmemcpy/Paket.VisualStudio)

![PAKET](images/paket-visualstudio.png)

---

#### Paket - Project Principles:

* Integrate well into the existing NuGet ecosystem
* Make things work with minimal tooling (plain text files)
* Make it work on all platforms
* Automate everything
* Create a nice community

![PAKET](images/qa.jpeg)

***

## Thank you!

* Presentation Source: https://github.com/marcio-azevedo/presentations
* Gists: https://gist.github.com/marcio-azevedo/9576969640a404fd2944aab89117d212

* References:
    * https://fsprojects.github.io/Paket/
    * https://russcam.github.io/paket-fake-talk/#/intro
    * http://forki.github.io/PaketIntro/#/