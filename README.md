# transparentdogfood.dev

## Starting from scratch
hugo new site transparentdogfood.dev
cd transparentdogfood.dev
git submodule add https://github.com/vaga/hugo-theme-m10c.git themes/hugo-theme-m10c

hugo new content content/posts/my-first-post.md

hugo server --buildDrafts

## Running a local instance to test changes
hugo server -D