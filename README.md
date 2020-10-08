# Carla Challenge in Mcity

## Where does the challenge take place?
The challenge will be held inside the [Carla](https://carla.org/) version of [Mcity](https://mcity.umich.edu/). Mcity is a 32-acre proving ground for the testing of connected and automated vehicles located on the University of Michigan in Ann Arbor, Michigan. We build the Carla Mcity based on the true dimensions/background of the real Mcity, and it serves as just another map of the Carla simulator. The supported Carla version is [0.9.9.4](https://github.com/carla-simulator/carla/tree/0.9.9.4). To learn more about the Carla simulator, please check out the [official documentations](https://carla.readthedocs.io/en/latest/).

<img src="resource/Mcity11.png" alt="drawing" width="700"/>
<img src="resource/Map.png" alt="drawing" width="700"/>



## What are the challenges?
<img src="resource/Route.png" alt="drawing" width="400"/>

The participant will be asked to control the vehicle under test (VUT) ('role_name' = "hero", spawned by the organizer) to follow a nominal route, shown as the blue curve in the figure. There will be 4 scenarios along the way, where the environment vehicles/pedestrian will attempt to challenge the VUT:
1. Cut-in
2. Car-following
3. Pedestrian crossing
4. Unprotected left turn

<img src="resource/scenarios1.png" alt="drawing" width="700"/>
In each run, only one participating team will control the VUT. All the environment vehicles/pedestrian are controlled by a challenge script running on the server, which is provided by the University of Michigan. The parameter of each scenario will be randomly sampled from its parameter space according to some given challenge level. The VUT will be graded based on safety, average speed and smoothness when driving along the route. Details on scoring system will be announced soon.

Here is an example run of the challenge. Click the picture to check out the video on YouTube. 
[![SampleRun](resource/videoclip.png)](https://www.youtube.com/watch?v=rw22kinHzqM)

The nominal route for the challenge can be found in the github repo. 

## How to participate?
### Remote connection
The simulator server and challenge script will be running on a dedicated server at University of Michigan. Participant are asked to remotely connect to the server through SSH tunnel with key authentication. Currently, the challenge is open to student teams from Stanford Univeristy, Massachusetts Institute of Technology and University of Michigan. 

To establish a SSH tunnel, one can use the command listed below (take MIT team as example)
```bash
ssh mit@141.211.37.251 -L 2000:localhost:2000 -L 2001:localhost:2001 -L 2002:localhost:2002
```
See the table below for the name of user assigned to the teams
|User Name|Team|
|---|---|
|`mit`| Massachusetts Institute of Technology |
|`stanford`| Stanford University |

Once the SSH tunnel is set up, you can connect to the server as if it is running on your computer. We set the connection limitation such that only one logins across the teams could be established. So if you find SSH says `Too many logins for xxx`, that indicates that other team are connecting to the server. We make sure that only one team can connect to the server and evaluate their agent at the same time through this way. Also note that this also means each user can only have one login shell at the same time. Please use utils like `tmux` if you need multiple shells. Please also make sure that you terminated the login shell correctly so that other teams can connect in.

By default, Carla will use port 2000/2001. To enable relevant command sent to the server, we preserve the port 2002 for commands including restarting Carla server, challenge script, etc. Therefore, you can add tunnel for 2002 when connecting. Here is the code for sending command to control the challenge script to start at different points:

```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('localhost', 2002))
print(s.recv(1024))
# See table below for meanings of the value
data = bytes('1', 'utf8')
s.send(data)
s.close()
```

Current implemented commands include
<!--
|Binary Value| Command|
|----|----|
|1| Initiate a test run from the start|
|2| Initiate the pedestrian crossing & left turn challenge|
|3| Initiate the left turn challenge|-->
- '1': Initiate a test run from the start
- '2': Initiate the pedestrian crossing & left turn challenge
- '3': Initiate the left turn challenge


To start a test run, you should first run the code above the launch the challenge script, then start your controller to control the VUT.

### A provisional schedule 
To avoid conflicts on server connection, we made a simple schedule for all teams to access the server:

For initial testing and debugging, Stanford team can connect on Oct 8, while MIT team can connect on Oct 9. Starting from the week of Oct 12, the MIT team can connect on Monday & Wednesday, the Stanford team can connect on Tuesday & Thursday, while Michigan team on Friday.

### Contacts 
If you are interested in joining in the challenge, please first contact Yuanxin Zhong(zyxin@umich.edu) or Xinpeng Wang(xinpengw@umich.edu) to get access to the server.


<!-- ## Welcome to GitHub Pages

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

-->
