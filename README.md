# LibGit2Sharp

[![CI](https://github.com/libgit2/libgit2sharp/actions/workflows/ci.yml/badge.svg)](https://github.com/libgit2/libgit2sharp/actions/workflows/ci.yml) 
[![NuGet version (LibGit2Sharp)](https://img.shields.io/nuget/v/LibGit2Sharp.svg)](https://www.nuget.org/packages/LibGit2Sharp/)

**LibGit2Sharp brings all the might and speed of [libgit2](http://libgit2.github.com/), a native Git implementation, to the managed world of .NET**

## Online resources

- [NuGet package](http://nuget.org/List/Packages/LibGit2Sharp)
- [Source code](https://github.com/libgit2/libgit2sharp/)

## MadCap steps for building locally

1. Clone this repository as well as libgit2sharp.nativebinaries so they are in folders next to each other:

	```
	git clone https://github.com/madcapsoftware/libgit2sharp.git
	git clone https://github.com/madcapsoftware/libgit2sharp.nativebinaries.git
	```

	Example folder structure:
	
	```
	C:\source\madcapsoftware\libgit2sharp
	C:\source\madcapsoftware\libgit2sharp.nativebinaries
	```

2. Open a powershell terminal to the root of the libgit2sharp.nativebinaries repository
3. Build `libgit2sharp.nativebinaries` and create a local nuget package, specifying the version to use. The version at time of writing matches the main `libgit2sharp.nativebinaries` repository with a `-ssh` suffix.

    ```
    .\UpdateAllLibsToSha.ps1 -libgit2sha main -libssh2sha master -zlibsha master
    .\build.libgit2.ps1 -x86 -x64 -libssh2
    .\nuget.exe Pack nuget.package/NativeBinaries.nuspec -Version 2.0.320-ssh -NoPackageAnalysis
    ```

4. Open the LibGit2Sharp solution
5. Right click the LibGit2Sharp project and click "Manage NuGet packages..."
6. Make sure "Package source" is set to "libgit2sharp.nativebinaries" which is a local relative path to the package generated in step 3
7. Check "Include prerelease" as the package version is a prerelease version due to the `-ssh` suffix
8. Click Install to update to the latest version
9. Build the `Release` solution configuration.

NOTE: The version of the resulting dll is based on the most recent git tag, which in this case is `0.27.2-ssh.0`.
For more details, see: https://github.com/adamralph/minver

## Troubleshooting and support

- Usage or programming related question? Post it on [StackOverflow](http://stackoverflow.com/questions/tagged/libgit2sharp) using the tag *libgit2sharp*
- Found a bug or missing a feature? Feed the [issue tracker](https://github.com/libgit2/libgit2sharp/issues)
- Announcements and related miscellanea through Twitter ([@libgit2sharp](http://twitter.com/libgit2sharp))

## Quick contributing guide

- Fork and clone locally
- Create a topic specific branch. Add some nice feature. Do not forget the tests ;-)
- Send a Pull Request to spread the fun!

More thorough information is available in the [wiki](https://github.com/libgit2/libgit2sharp/wiki).

## Optimizing unit testing

LibGit2Sharp strives to have a comprehensive and robust unit test suite to ensure the quality of the software and to assist new contributors and users, who can use the tests as examples to jump start development. There are over one thousand unit tests for LibGit2Sharp, and this number will only grow as functionality is added.

You can do a few things to optimize running unit tests on Windows:

1. Set the `LibGit2TestPath` environment variable to a path in your development environment.
    * If the unit test framework cannot find the specified folder at runtime, it will fall back to the default location.
2. Configure your anti-virus software to ignore the `LibGit2TestPath` path.
3. Install a RAM disk like [IMDisk](http://www.ltr-data.se/opencode.html/#ImDisk) and set `LibGit2TestPath` to use it.
    * Use `imdisk.exe -a -s 512M -m X: -p "/fs:fat /q /v:ramdisk /y"` to create a RAM disk. This command requires elevated privileges and can be placed into a scheduled task or run manually before you begin unit-testing.

## Authors

- **Code:** The LibGit2Sharp [contributors](https://github.com/libgit2/libgit2sharp/contributors)
- **Logo:** [Jason "blackant" Long](https://github.com/jasonlong)

## License

The MIT license (Refer to the [LICENSE.md](https://github.com/libgit2/libgit2sharp/blob/master/LICENSE.md) file)
