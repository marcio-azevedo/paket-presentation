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

' Problems: path to packages changes at every update, code reviews are harder because you're always updating csproj files, etc

---

### Updates may require manual work (specially if you update framework)

![PAKET](images/csproj-references.png)

' Neither Visual Studio neither NuGet are clever to update it when you change the project Framework.

***

#### Main components

* paket.exe (~/.paket directory in root)
* paket.dependencies (in solution root) - Global definition of dependencies
* paket.lock (generated from paket install) - List of used versions for all dependencies
* paket.references (in each project folder) - Dependency definition per project, "replaces" packages.config
* paket.template - Package definition for new packages

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
