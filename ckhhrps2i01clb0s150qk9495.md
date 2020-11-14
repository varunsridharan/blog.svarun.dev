## Github Markdown Syntax Guide

[Markdown](http://daringfireball.net/projects/markdown/) is a way to style text on the web. You control the display of the document; formatting words as bold or italic, adding images, and creating lists are just a few of the things we can do with Markdown.

Github has created its own [Flavor of Markdown](https://github.github.com/gfm/).
You can use GitHub Flavored Markdown anywhere in the Github Ecosystem

- Github
- Gists
- Github Pages
- Github Discussions
- Issues
- Pull Requests


In this post, I am sharing the full list of supported markdown syntax in Github
let's get started with the basics


## [Headings](https://github.com/varunsridharan/blog-demos/blob/main/github-markdown-syntax-guide/heading.md)
You can use one `#` up to `######` six for different heading sizes.

```markdown
# Heading 1
## Heading 2
### Heading 3
### Heading 4 
#### Heading 5
###### Heading 6
```
![Headings](https://s2.do-spaces.com/2020/Nov/14/1605357103-158.jpg)

---

## [Text Styling](https://github.com/varunsridharan/blog-demos/blob/main/github-markdown-syntax-guide/text-style.md)
Text in the markdown can be styled with the below syntax

```markdown
[link to Google!](http://google.com)

[link to Google With Title](http://google.com "Hi, I am the title" )

**Bold Text**

*Italic Text*

***Bold & Italic***

~I am Striked Out~

This line has an `inline` code block

> Blockquoted Text

>> Nested Block Quote Possible 

>>> Unlimited Level Of Blockquote Nesting
```

![Text Styling](https://s2.do-spaces.com/2020/Nov/14/1605358824-169.jpg)

---

### Links
Adding links in a markdown can sometimes become hard especially when working on a large markdown file. and for that markdown has provided an awesome feature where you can globally set the links for a word and then use that word to call it as a link.

```markdown
Inline linking [Github](https://github.com)
Linking [Google] & [Hashnode] using globally set links

Link with [Custom title](https://example.com "This is an awesome website")

[Google]: http://google.com
[Hashnode]: http://hashnode.com
```
---

## [Lists](https://github.com/varunsridharan/blog-demos/blob/main/github-markdown-syntax-guide/lists.md)
Creating a list in markdown is quite easy as just appending a single character
for unordered list append `*` or `-` 
for ordered list append `1.` 


```markdown
### Unordered List
List using `*`
* Item 1
* Item 2

List using `-`
- Item 1
- Item 2


### Ordered List

1. Item 1
1. Item 2
1. Item 3

### Nested Lists

* Unordered List
  - Sub item 1
  - Sub item 2
* Ordered List
  1. Sub Item 1
  1. Sub Item 2

```

![Working With Lists](https://s2.do-spaces.com/2020/Nov/14/1605358056-163.jpg)

---

## [Images](https://github.com/varunsridharan/blog-demos/blob/main/github-markdown-syntax-guide/images.md)
adding images in markdown is fairly easy by just adding `![Alt Text](Image URL)`

```markdown
### Basic Image
![Basic Image](https://avatars1.githubusercontent.com/u/583231)


### Image With HTML Title Attribute
![Image With Title](https://avatars1.githubusercontent.com/u/583231 "The Octocat Avatar")

```
> Yes Github Supports HTML Title Tag In Images

![Working With Images](https://s2.do-spaces.com/2020/Nov/14/1605358698-126.jpg)

---


## [Tables](https://github.com/varunsridharan/blog-demos/blob/main/github-markdown-syntax-guide/table.md)
You can create tables by assembling a list of words and dividing them with hyphens `-` (for the first row), and then separating each column with a pipe `|`
```markdown
| First Header | Second Header |
| --- | --- |
| Content from cell 1 | Content from cell 2 |
| Content in the first column | Content in the second column |
```
![Working With Tables](https://s2.do-spaces.com/2020/Nov/14/1605359151-146.jpg)

### Table Column Alignment
In markdown, each table column text can be assigned `left`,` right, or `center` alignment using the below options

1. For Left Align `:--` 
2. For Center Align `:---:`
3. For Right Align `---:`

```markdown
`Column 2` is Right aligned 

| Column 1 | Column 2 | Column 3 |
| --- | ---: | --- |
| Content | I am right aligned | Content |
| Content | I am right aligned | Content |
| Content | I am right aligned | Content |

`Column 2` is Right aligned 

| Column 1 | Column 2 | Column 3 |
| --- | ---: | --- |
| Content | I am right aligned | Content |
| Content | I am right aligned | Content |
| Content | I am right aligned | Content |

`Column 2` is Left aligned 

| Column 1 | Column 2 | Column 3 |
| --- | :--- | --- |
| Content | I am left alinged | Content |
| Content | I am left alinged | Content |
| Content | I am left alinged | Content |
```
![Working With Tables](https://s2.do-spaces.com/2020/Nov/14/1605359591-116.jpg)

---

## GitHub Flavored Markdown
Github has explained well so please refer to [GitHub Flavored Markdown Docs](https://guides.github.com/features/mastering-markdown/#GitHub-flavored-markdown) on how to use Codeblocks,Task Lists,SHA references,Username @mentions & Emoji

%[https://github.com/varunsridharan/blog-demos/tree/main/github-markdown-syntax-guide]

%%[blog-footer]