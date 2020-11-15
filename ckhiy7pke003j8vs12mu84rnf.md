## Github Markdown Style Guide

In the [previous post](https://blog.svarun.dev/github-markdown-syntax-guide) in this series, we learned how to write markdown in Github and its exclusive features. 

In this post, we are going to learn how we can style our `README.md`

## [Text Align](https://github.com/varunsridharan/blog-demos/blob/main/2020/11/Github%20Markdown%20Style%20Guide/text-align.md)
Using `align="left"` attribute text can be aligned easily and it works with all the tags that markdown supports.

```markdown
## Text Align - <p>
<p align="center">This is center aligned!</p>
<p align="left">Left aligned</p>
<p align="right">Right aligned</p>


## Text Align - <div>
<div align="center">This is center aligned!</div>
<div align="left">Left aligned</div>
<div align="right">Right aligned</div>
```
#### Github Output
> ![Text Align](https://s2.do-spaces.com/2020/Nov/15/1605431390-1100.jpg)


---

## [Image Align](https://github.com/varunsridharan/blog-demos/blob/main/2020/11/Github%20Markdown%20Style%20Guide/image-align.md)

```markdown
## Left Align
<p ><img align="left" width="200" src="https://via.placeholder.com/400x200"></p>

<br/><br/><br/><br/>

## Right Align
<p ><img align="right" width="200" src="https://via.placeholder.com/400x200"></p>

<br/><br/><br/><br/>

## Center Align
<p align="center" ><img width="200" src="https://via.placeholder.com/400x200"></p>
```

#### Github Output
> ![Image Align](https://s2.do-spaces.com/2020/Nov/15/1605432179-180.jpg)

---

## [List With indentation](https://github.com/varunsridharan/blog-demos/blob/main/2020/11/Github%20Markdown%20Style%20Guide/list-with-indentation.md)

```html
# List With indentation

<dl>
  <dt>List Item 1</dt>
  <dd>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris pharetra, ante vitae gravida rhoncus, nunc nulla posuere felis</dd>
  <dt>List Item 2</dt>
  <dd>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris pharetra, ante vitae gravida rhoncus, nunc nulla posuere felis</dd>
</dl>


# Nested List With indentation
<dl>
  <dt>List Item 1</dt>
  <dd>
    Lorem ipsum dolor sit amet
    <dl>
      <dt>Nested List Item 1</dt>
      <dd>
        Lorem ipsum dolor sit amet
        <dl>
          <dt>Nested List Item 2</dt>
          <dd>Lorem ipsum dolor sit amet</dd>
        </dl>  
      </dd>
    </dl>
  </dd>
</dl>
```
#### Github Output
> ![List With Indentation](https://s2.do-spaces.com/2020/Nov/15/1605432607-186.jpg)

---

## [Dropdown](https://github.com/varunsridharan/blog-demos/blob/main/2020/11/Github%20Markdown%20Style%20Guide/dropdown.md)
To Make Markdown work inside `details` tag make sure to leave the empty line after the summary tag

> **Dropdown** in markdown supports all the basic features such as Text, Image, Table, List, .etc inside. i am just show some of it. not all.


### Text
```markdown
<details>
  <summary>Dropdown With Text</summary>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris pharetra, ante vitae gravida rhoncus, nunc nulla posuere felis, 
  id rhoncus ante tellus malesuada libero. Aliquam fermentum massa eget sodales aliquet.
  Morbi vitae velit tincidunt lorem fringilla lacinia non vitae leo. Fusce congue odio eget tellus finibus vulputate. 
</details>
```

#### Github Output
> ![Text Dropdown](https://s2.do-spaces.com/2020/Nov/15/1605433339-129.gif)

### Image
```markdown
<details>
  <summary>Dropdown With Image</summary>
 
  ![Image Here](https://via.placeholder.com/600x200)  
</details>
```

#### Github Output
> ![Image](https://s2.do-spaces.com/2020/Nov/15/1605433474-117.gif)


### Table
```markdown
<details>
  <summary>Dropdown With Table</summary>

  | First Header | Second Header |
  | --- | --- |
  | Content from cell 1 | Content from cell 2 |
  | Content in the first column | Content in the second column |
  
</details>
```
#### Github Output
> ![Table](https://s2.do-spaces.com/2020/Nov/15/1605433559-135.gif)

---

You can check out the live demo @ this repository

%[https://github.com/varunsridharan/blog-demos/tree/main/2020/11/Github%20Markdown%20Style%20Guide]

---



%%[blog-footer]