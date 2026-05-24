# My Awesome Tech Blog

This is a simple, static tech blog powered by [Hugo](https://gohugo.io/) and deployed automatically to [Cloudflare Pages](https://pages.cloudflare.com/) via GitHub Actions.

## Getting Started Locally

To run this blog on your local machine, follow these steps:

### Prerequisites

Make sure you have [Hugo](https://gohugo.io/getting-started/installing/) installed on your system. You can verify your installation by running:

```bash
hugo version
```

### Run the Blog

1.  **Clone the repository:**
    ```bash
    git clone [YOUR_REPOSITORY_URL]
    cd blog # Or whatever your repository directory is named
    ```

2.  **Start the Hugo development server:**
    ```bash
    hugo server
    ```

    Hugo will build the site and serve it, usually accessible at `http://localhost:1313/` in your web browser. It will automatically reload the page when you make changes to your content or templates.

## Adding New Blog Posts

To create a new blog post:

1.  **Generate a new post file:**
    ```bash
    hugo new posts/my-awesome-new-post.md
    ```
    This will create a new Markdown file in `content/posts/` with pre-filled [front matter](https://gohugo.io/content-management/front-matter/).

2.  **Edit the post:** Open the generated `.md` file and add your content. Remember to set `draft: false` in the front matter when you are ready to publish it.

    Example `content/posts/my-awesome-new-post.md`:
    ```markdown
    ---
    title: "My Awesome New Post"
    date: 2026-05-24T12:00:00-05:00
    draft: false
    categories: ["Technology"]
    tags: ["hugo", "cloudflare"]
    ---

    This is the content of my new blog post. It's written in Markdown.
    ```

3.  **Commit and Push:** Once you're happy with your post, commit the changes and push to your `main` branch. This will trigger the deployment via GitHub Actions.

## Deployment to Cloudflare Pages

The blog is configured to automatically deploy to Cloudflare Pages whenever changes are pushed to the `main` branch of this GitHub repository.

### Cloudflare API Tokens (GitHub Secrets)

For the deployment to work, you need to provide your Cloudflare API Token and Account ID as [GitHub Repository Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets):

1.  **Navigate to your GitHub repository** on GitHub.com.
2.  Go to `Settings` > `Secrets and variables` > `Actions`.
3.  Click on `New repository secret` and add the following two secrets:
    *   `CLOUDFLARE_API_TOKEN`: 
        *   **Where to get it:** Log in to your Cloudflare dashboard, go to "My Profile" (top right corner), then "API Tokens". Create a new token with at least "Cloudflare Pages: Edit" permissions. **Do NOT use your Global API Key for this.**
    *   `CLOUDFLARE_ACCOUNT_ID`: 
        *   **Where to get it:** This can be found in your Cloudflare dashboard. Select your account, then on the right sidebar, under "API" section, you'll see "Account ID".

    The `GITHUB_TOKEN` secret is automatically provided by GitHub Actions and does not need to be manually added.

### Cloudflare Pages Project Name

Ensure that the `projectName` in the GitHub Actions workflow (`.github/workflows/deploy.yml`) matches the name of your project in Cloudflare Pages. It is currently set to `my-awesome-tech-blog`:

```yaml
          projectName: my-awesome-tech-blog # Replace with your project name in Cloudflare Pages
```

Once these secrets are set and the project name is correct, any push to the `main` branch will automatically build your Hugo site and deploy it to Cloudflare Pages!