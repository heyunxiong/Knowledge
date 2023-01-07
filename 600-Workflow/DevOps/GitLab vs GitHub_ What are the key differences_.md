![image.png](_assets/GitLab%20vs%20GitHub_%20What%20are%20the%20key%20differences_/1616946453872-c94fffcb-af1d-43ba-8897-652b1576563a.png)
> _This article is brought to you by _[_Usersnap_](https://usersnap.com/classic/?gat=blog-post)_. Usersnap helps you to communicate visually. And the best part? It connects with _[_GitLab_](https://usersnap.com/integrations/gitlab/?gat=blog-post)_ and _[_GitHub_](https://usersnap.com/integrations/github/?gat=blog-post)_. _
> _ref: _[https://usersnap.com/blog/gitlab-github/](https://usersnap.com/blog/gitlab-github/)



Version Control repository management services are a key component in the software [development workflow](https://usersnap.com/blog/development-workflow/). In the last few years, GitHub and GitLab positioned themselves as handy assistants for developers, particularly when working in large teams.

With the latest release of GitLab 10.0, GitLab took a major leap forward from code management, to deployment and monitoring. GitLab calls it Complete DevOps. They aim for the entire software development, deployment, and DevOps market.

That means when talking about the differences and similarities of GitLab vs GitHub, we need to look beyond code repositories and take a look at the entire process.
Ready?
## Git explained
Both, GitLab and GitHub are web-based Git repositories.
**What is a Git Repository?**
The aim of Git is to manage software development projects and its files, as they are changing over time. Git stores this information in a data structure called a repository.
Such a git repository contains a set of commit objects and a set of references to commit objects.
A git repository is a central place where developers store, share, test and collaborate on web projects.
## More than a Git repository: How to Complete DevOps
Nowadays, GitLab and GitHub are more than “just” git repositories for developers.
GitLab says about their recently announce [Complete DevOps vision](https://about.gitlab.com/2017/10/09/gitlab-raises-20-million-to-complete-devops/):
> Now, we’re taking it a step further to unite development and operations in one user experience.

GitLab realized the need for better and deeper integrations between development and DevOps toolchains. With the latest release of 10.0, GitLab rethinks the scope of tooling for both developers and operation teams.
## The Basics of GitHub and GitLab
Let’s start with the basics. GitHub is a Git-based repository hosting platform with 40 million users (January 2020) making it the largest source code globally. Originally, GitHub launched in 2008 and was founded by Tom Preston-Werner, Chris Wanstrath, and PJ Hyett.

GitHub projects can be made public and every publicly shared code is freely open to everyone. You can have private projects as well, but only 3 collaborators allowed on the free plan.

Public repositories on GitHub are often used to share open source software. Besides the basic code repository, GitHub can be used for issue tracking, documentation, and wikis.

Overall, more than 100 million repositories have been created on GitHub in 2017.
Similar to GitHub, GitLab is a repository manager which lets teams collaborate on code. Written in Ruby and Go, GitLab offers some similar features for issue tracking and project management as GitHub.

Founded by Dmitriy Zaporozhets and Valery Sizov in 2011, GitLab employs more than 1,300 people and according to Wikipedia, GitLab has 100,000 users (March 2017) and is used by enterprises such as IBM, Sony, and NASA.
## Key differences and similarities: GitLab vs GitHub
According to various sources and our own experience, we identified the following **key differences** you should know when making the decision: **_GitLab vs GitHub_**.
## Authentication Levels
With GitLab you can set and modify people’s permissions according to their role. In GitHub, you can decide if someone gets a read or write access to a repository.

With GitLab you can provide access to the issue tracker (for example) without giving permission to the source code. This is obviously great for larger teams and enterprises with role-based contributors.
## **GitLab CI vs GitHub Actions**
One of the big differences between GitLab and GitHub is the built-in Continuous Integration/Delivery of GitLab. CI is a huge time saver for many development teams and a great way of QA (nobody likes pull requests that break your application).

GitLab offers its very own CI for free. No need to use an external CI service. And if you are already used to an external CI, you can obviously integrate with Jenkins, Codeship, and others.

GitLab has clearly been addressing the DevOps market earlier than its competitor as well as offering an operations dashboard that lets you understand the dependencies of your development and DevOps efforts.

GitLab CI offers [Auto DevOps](https://docs.gitlab.com/ee/topics/autodevops/) which automatically run CI/CD without a human being actually setting it up.
> But, really, every project should be running some kind of CI. So, why don’t we just detect when you’ve pushed up a project; we’ll just build it, and we’ll go and test it, because we know how to do testing.Mark Pundsack, source: [gitlab.com](http://gitlab.com)

So, how does CI / CD work inside the GitHub universe? GitHub released [Actions](https://github.com/features/actions) in late 2019, which essentially allows you to write tasks that automate and custom the development workflow. It’s also free to get started.
But GitHub does not come with a deployment platform and needs additional applications, such as Heroku.
Download for free this [step-by-step CI/CD pipeline set up guide](https://usersnap.com/e-books/ebook-ci-cd-gitlab-github) with GitLab vs. GitHub & Travis CI.
## Issue Tracking
GitLab, as well as GitHub, provide a simple issue tracker that lets you change status and assignee for multiple issues at the same time.

Both are great issue trackers, especially when connected with a visual bug tracker like [Usersnap](https://usersnap.com/classic/?gat=blog-post). While your developers still enjoy the great issue tracking interface of GitLab and GitHub, your testers, colleagues, and clients can simply report bugs through the Usersnap widget.

Bug reports and user feedback can automatically be sent to [GitLab](https://usersnap.com/integrations/gitlab/?gat=blog-post) or [GitHub](https://usersnap.com/integrations/github/?gat=blog-post). Or you can pre-filter those tickets inside Usersnap and manually send it to your development project.
## Import & Export
When thinking about moving to GitLab or GitHub, you should also consider the setup costs and resources needed for getting started. In that regard, the topic of available import and export features is pretty important.

GitLab offers [detailed documentation](https://docs.gitlab.com/ee/user/project/import/index.html) on how to import your data from other vendors – such as GitHub, Bitbucket – to GitLab.

GitHub, on the other hand, does not offer such detailed documentation for the most common git repositories. However, GitHub offers to use GitHub Importer if you have your source code in Subversion, Mercurial, TFS and others.
Also when it comes to exporting data, GitLab seems to do a pretty solid job, offering you the ability to export your projects including the following data:

- Wiki and project repositories
- Project uploads
- The configuration including webhooks and services
- Issues with comments, merge requests with diffs and comments, labels, milestones, snippets, and other project entities

GitHub, on the other hand, seems to be more restrictive when it comes to export features of existing GitHub repositories.
## Integrations
Both GitLab and GitHub offer a wide range of 3rd party integrations. Integrating your version control system with other application enriches your workflows and can boost productivity for your developers and your non-developers.
In order to check out if your favorite apps are compatible with GitLab and GitHub, I recommend checking out the documentation of GitLab and GitHub.
Besides the available integration partners, GitHub launched their GitHub marketplace in May 2017 offering you selected tools and applications.
GitLab took a similar path and offers multiple integrations for development and DevOps teams.
## The GitHub community
GitHub positioned itself among its community of developers. And its popularity is mainly driven by the highly active GitHub community of millions of developers. You can discuss problems and maybe learn a few unofficial but [awesome hacks](https://usersnap.com/blog/github-hacks-productivity/) there. On the other hand, GitLab undertook some great activities, such as hosting community events and connecting open source contributors.
If you’re looking for the biggest community of developers, chances are high that GitHub is the better place to be.
## GitLab Enterprise vs GitHub Enterprise
On an enterprise level, you should consider further factors when making an informed decision of whether to use GitLab vs GitHub.
GitHub is highly popular among developers, and over the last few years, it gained popularity among larger development teams and organizations too.
On the other hand, GitLab is pretty strong on enterprise features, too. With different enterprise plans available, GitLab is particularly popular among larger development teams.
Here is, how GitLab and GitHub compare on pricing.
While GitHub’s enterprise plan starts at 2,500 USD per 10 users per year (= 250 USD per user), GitLab’s enterprise starter plan is 39 USD per user/per year.
## Wrapping it up.
Undoubtedly, GitHub is still the most popular git repository with the largest number of users and projects. However, GitLab is doing a fantastic job offering your entire development (and DevOps) teams great tools for more efficient workflows.
## Bonus tip: Get user feedback & bug reports with Usersnap
Last but not least, I wanted to give you a heads-up on [Usersnap](https://usersnap.com/classic/?gat=blog-post), which is our very own visual user feedback and bug tracking tool, used by companies like Facebook and Microsoft.
And the best part? You can connect [GitHub issues](https://usersnap.com/integrations/github/?gat=blog-post) or [GitLab issues](https://usersnap.com/integrations/gitlab/?gat=blog-post) with Usersnap to get visual bug reports directly sent to your preferred system.
Get great user feedback & bug reports with a [free Usersnap trial](https://usersnap.com/classic/?gat=blog-post).
