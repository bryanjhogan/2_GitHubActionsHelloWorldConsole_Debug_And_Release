---
slug: github-actions-with-net-part-2-dependent-jobs
title: GitHub Actions with .NET, Part 2 - Dependent Jobs
date: "2021-04-30"
tags: [dotnet, GitHub Actions]
---

_Full source code available [here](media/xxxx.zip)_.

In the previous post I gave a quick introduction to GitHub Actions showing how to build a small Hello World application and make the artifact available for download. 

In this post I'll show how to build debug and release versions of the same application, with the release only being built if the debug one builds. 
This in itself is not a whole lot of use, but in the next post I'm going to show how to add manual approvals before performing certain jobs, like deploying built code to AWS. 

But for now, I'm keeping it simple without the complications of external services, secrets, environment variables, etc. 

### The Code
The C# is very simple, print a different piece of text depending on the build configuration.

{{< highlight csharp "linenos=true" >}}
class Program
{
    static void Main(string[] args)
    {
        #if DEBUG
            Console.WriteLine("Hello World! From debug build.");
        #endif
        #if RELEASE       
            Console.WriteLine("Hello World! From release build.");
        #endif
    }
}
{{< /highlight >}}

### Two Jobs in the GitHub Action Workflow
In the previous post there was only one job, but you can have as many as you want, and these jobs can have dependencies on each other, i.e. if job 1 fails, don't run job 2. 



