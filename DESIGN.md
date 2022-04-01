# Preface
JAMStack is useful, and to be more precise, one of its tools — Hugo — does its job very well. It does only one job — rendering some predefined content, so you need to prepare your texts using available editor of choice or your Git provider web interface. Currently we don't have some mainstream solution to edit files for Hugo collaboratively and without authentication, so “wiki-style” editing, open and anonymous CMS is impossible.

And here comes “derpedit” — as a concept for now.

# derpedit
```
Usage: derpedit [OPTION]

Options:
	--bind TEXT	The IP to bind the server to.  [default: ::1, 127.0.0.1]
	--port INTEGER	Port of the web server. [default: 80]
	--storage [github|git|local]
	--content-directory DIRECTORY	Directory to use for Hugo content. [default: ./content]
	--storage-git-username TEXT	Default username to use when creating commits. [default: Librarian]
	--storage-git-email TEXT	Default email to use when creating commits. [default: wiki@localhost]
	--storage-github-url URL        Repository URL on GitHub.  [default: https://github.com/innereq/derpedit-example]
	--storage-github-history-url URL	Repository URL on GitHub to visit history (defaults to --storage-github-url).
	--storage-github-private-key TEXT	Base64-encoded private key to access GitHub. Always use this via an environment variable!
	--storage-github-branch branch  Branch of the GitHub repository to use. [default: main]
```

`derpedit` is a companion tool to main `hugo` binary. It's used for manipulating contents of your Hugo static website, like: viewing source directory with its contents, viewing source of individual files, editing contents of files, uploading images and other media in article's directory, viewing file revisions etc.

## Default
By default `derpedit` looks for a Git repository in current local working directory, if it doesn't exist and Git provider URL isn't provided the program must throw an error. If it exist, the program starts a web server and listens to HTTP requests, like GET and POST, and shows contents of the `--content-directory`.

When some change is commited, the program launches `hugo` binary in current working directory to build our site. IF Git provider URL is specified, the program launches `git push` or similar programming language function (e.g. cgit2 bindings). If it's not provided, the program just launches `git commit` or similar.

## --storage-github-url
If Git provider URL is specified, the program launches `git clone` or similar to clone the repository in current working directory and work with it. When some change is commited, the program launches `git commit` and `git push` or similar and pushes changes to the Git provider URL using provided credentials. When URL is provided, web interface shows “history” button on files which directs to Git provider history URL (e.g. GitHub file commits history).

## Content
Users of the program must use media files in article directories, e.g.

```
content/
	some-article-name/
		index.md
		attachment1.jpg
		attachment2.webm
```

## Commiting
When started correctly, the program starts a web server. Users see listing of `--content-directory`: a simple list of files they can click on; “Add” button to create a new article directory with `index.md` in it; “Upload” button to upload attached media to an article when browsing the article directory. Clicking on `index.md` shows editor, so users can see source of the file and edit it if they want to do so; if Git provider URL is specified, there is “History” button behind the text field which directs to e.g. GitHub file commits history.

# Misc
## References
- https://github.com/TrueBrain/TrueWiki
- https://github.com/gollum/gollum
- http://source.ikiwiki.branchable.com/?p=source.git;a=tree
