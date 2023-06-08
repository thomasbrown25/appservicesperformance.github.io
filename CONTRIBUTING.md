## Access

You will need write access to create pull request. Email your TA to gain access to <https://github.com/Appservicesperformance/appservicesperformance.github.io>

## Environment Setup

1. Download and install the Ruby development kit
2. Download and install Visual Studio Code

## Git from VS Code

1. Fork the project from GitHub <https://github.com/Appservicesperformance/appservicesperformance.github.io>
2. Clone the project using VS Code

```bash
git clone https://github.com/<username>/appservicesperformance.github.io.git
```

NOTE:  Tutorial can be found at <https://github.com/firstcontributions/first-contributions/blob/master/github-windows-vs-code-tutorial.md>

## Jekyll

5. Install any missing Ruby gems:

```bash
bundle install
```

6. Run the local Jekyll server. From the project directory, run the following command:

```bash
bundle exec jekyll serve
```

   The blog will be running at <http://127.0.0.1:4000/>

   VSCODE: If you are using VSCode to author your blog post, please install Markdown Linting extension

## Authoring your post

1. Create a new branch for your article(s).

- If you are not comfortable on the command line, download GitHub Desktop.
- See <https://github.com/firstcontributions/first-contributions/blob/master/github-windows-vs-code-tutorial.md#create-a-branch> for steps using VS Code

2. Create a markdown file under the _posts directory with the following file name format: `YYYY-MM-DD-Your-Article-Title.md`.

3. Add the following to the top of your posts:

    ```yaml
    ---
    title: "Title should be the same (or similar to) your filename"
    author_name: "Your Name"
    tags:
        - example
        - multiple words
        - no more than 3 tags
    categories:
        - <Service Type> # Azure App Service on Linux, Azure App Service on Windows
        - <Stack> # Python, Java, PHP, Nodejs, Ruby, .NET Core
        - <Blog Type> # How-To, Diagnostics, Configuration, Troubleshooting, Performance
    header:
        teaser: "/assets/images/imagename.png" # There are multiple logos that can be used in "/assets/images" if you choose to add one.
    # If your Blog is long, you may want to consider adding a Table of Contents by adding the following two settings.
    toc: true
    toc_sticky: true
    date: YYYY-MM-DD 00:00:00
    ---
    ```

The tags section is optional.

## Digital Content

To add images, GIFs, or other digital content to your post...

1. Add the file under the `/media/YEAR/Topic/` directory.

- Where `YEAR` and `MONTH` are the year and month in your article's filename. If the directory for the year or month does not yet exist, please create them.

2. Once the file is added, you can link to the file in your markdown using the path `/media/YEAR/Topic/your_file_name.jpg`. For example, to insert an image in Markdown you would use the following syntax

```text
![Required description of the image](/media/2019/04/portal-picture.jpg)
```

Publishing

 1. Proofread your post for spelling and grammar
  ○ Pro-Tips: Copy/paste your content into Word to check spelling. Also, install the VSCode Markdown Linting extension.
 2. Submit a pull request
