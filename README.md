# Chirpy Starter
## Introduction
Hello everyone! I'm Jiacheng Xu, a student majoring in Mathematics at Shanghai University.
This repository serves as my personal blog website. I plan to record snippets of my daily life, personal growth, career insights, as well as the knowledge and techniques I have learned here.

## How to Launch the Website
### Start Docker Container
```Powershell
docker start [containerID]
```

### Open Blog Repository with VS Code in Container
1. Press **F1** to open the command palette.
2. Search and select the command below:
    ```plaintext
    Dev Containers: Attach to Running Container...
    ```
3. Choose the running Jekyll container.
4. Wait a few seconds, and VS Code will open a new window and directly enter the internal environment of the container.

### Open the Blog Root Folder
In the newly opened VS Code window:
Navigate to `File → Open Folder`, then enter the path:
```plaintext
/workspaces/jiacheng-952.github.io
```

## How to Publish a Blog Post
### Write a New Post
Create a new Markdown file in the `/_posts` directory.
The file naming convention: `YYYY-MM-DD-post-title.md`, separated by hyphens, for example: `2026-05-02-hello-world.md`.

Add **Front Matter** at the top of the Markdown file. It tells Jekyll the basic information of the article such as title, category and layout.
```yaml
---
title: Your Article Title
date: 2026-02-05 14:00:00 +0800
categories: [MainCategory, SubCategory]
tags: [Tag1, Tag2]
author: Jiacheng-952  # Optional: Specify custom author
math: true            # Optional: Enable LaTeX math formula support
mermaid: true         # Optional: Enable Mermaid flowchart support
pin: false            # Optional: Set true to pin the post to homepage
---
```

Write your blog content in standard Markdown syntax below the Front Matter.

#### Image Insertion Rule
Use the following format to insert images:
```markdown
![Image Description](/assets/img/your-image-name.png)
```
Note: The path must start with `/`, which represents the root directory of the blog site.

Store all images corresponding to the post in this directory:
`/assets/img/post/2026-05-02-hello-world`

### Local Preview & Online Deployment
Finish writing the post and preview locally first before pushing to GitHub.

1. **Local Preview**
Run the following command in the VS Code terminal:
```bash
bash tools/run.sh
```
Visit `http://127.0.0.1:4000` in your browser to check layout, math formulas and image display.

2. **Publish Online**
If everything looks normal, execute the standard Git workflow:
```bash
git add .
git commit -m "Add new post: article brief description"
git push
```

3. **Wait for Deployment**
Wait about 1–2 minutes until GitHub Actions workflow completes with a green status. Your new blog post will then be automatically published and visible on the homepage.

---

[![Gem Version](https://img.shields.io/gem/v/jekyll-theme-chirpy)][gem]&nbsp;
[![GitHub license](https://img.shields.io/github/license/cotes2020/chirpy-starter.svg?color=blue)][mit]

When installing the **Chirpy** theme via [RubyGems.org][gem], Jekyll can only read files from the theme gem within the directories `_data`, `_layouts`, `_includes`, `_sass`, `assets`, along with partial configuration options in `_config.yml`.
If you have installed the Chirpy theme gem locally, run `bundle info --path jekyll-theme-chirpy` to locate the theme file path.

The Jekyll official design intends to grant users more customization flexibility, but this restriction prevents users from experiencing an out-of-the-box full-featured Chirpy theme.

To utilize all built-in features of **Chirpy**, you need to copy critical configuration and layout files from the theme gem to your local Jekyll site manually. The required core files and folders are listed below:
```shell
.
├── _config.yml
├── _plugins
├── _tabs
└── index.html
```

To save your time and avoid missing critical files during manual copying, we have extracted the latest stable theme configurations and integrated the continuous deployment workflow from the official **Chirpy** theme into this repository. You can start writing blog posts directly without extra configuration.

## Usage
Refer to the official documentation of the Chirpy theme: [Theme Wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

## Contributing
This repository is automatically synchronized with official new releases of the Chirpy theme. If you encounter any bugs or have feature suggestions, please submit feedback to the [official theme repository][chirpy].

## License
This project is open-sourced under the [MIT][mit] License.

[gem]: https://rubygems.org/gems/jekyll-theme-chirpy
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy/
[mit]: https://github.com/cotes2020/chirpy-starter/blob/master/LICENSE

