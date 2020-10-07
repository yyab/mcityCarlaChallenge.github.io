# Carla Challenge in Mcity

## Where does the challenge take place?
The Mcity map in Carla
<img src="resource/Map.png" alt="drawing" width="400"/>
## What are the challenges?
<img src="resource/Route.png" alt="drawing" width="400"/>

There will be 4 challenging scenarios along the way:
1. Cut-in
2. Car-following
3. Pedestrian crossing
4. Left turn
## How to participate?
SSH connection:
IP address: 
Remote control the script:

```markdown
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('localhost', 2002))
print(s.recv(1024))
# 1 for initializing from start; 2 before the pedestrian crossing; 3 before the left turn
data = bytes('1', 'utf8')
s.send(data)
s.close()
```


## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/yyab/mcityCarlaChallenge.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/yyab/mcityCarlaChallenge.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
