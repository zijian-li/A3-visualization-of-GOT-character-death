# A3-visualization-of-GOT-character-death

In this repo, we created four interactive visualization on death of characters in the hit series Game of Throne. Through the d3-based visualization, we want to help audiences to explore two key aspects of the dataset: 1) which character, or which group/house, suffered more death, or killed more people? 2) what’s the timeline of death, eg. when did the character die in the book or the series? We implemented directed graph and arc diagram for the first aspect, scatter plot and parallel coordinate plot for the second aspect. 

## Rationale for design desicions:
### Character Death and Killing in each house(Directed Graph)
1.1 Visual encoding:
This visualization gives the overview of character death and killing relationship in a directed graph. Each character is encoded as a node floating in the directed force graph. The edges in the directed graph represent the kills between the characters, with an arrow going from the killer to the victim. The color of the node is assigned according to the group of the character (defined as the primary house of the character, e.g. Catelyn Stark is of house Stark and Tully, and is assigned to group Stark; Cersei Lannister is of house Lannister and Baratheon, and is assigned to group Lannister). The character name and house are encoded in the tooltips, which appear at mouse hovering, giving richer information. 

1.2 Interaction techniques:
The main interactions in the force directed graph are tooltips and dragging. Since showing all the information about the characters on the screen would reduce the aesthetic cleanness of the network, the information is hidden until mouse hovering. The dragging technique is an interesting to interact with, and it helps to focus on the nodes of interest. The full graph contains about 400 nodes and edges, which may overlap or make the killing chain and network unclear. The dragging feature helps to clear off irrelevant nodes and edges and focus on the ones of interest.

1.3 Design rationale:
The Game of Thrones is famous for dramatic death of characters due to killing. The killing relationships between the characters can be complicated after 7 seasons, it would be helpful to visualize them in a full directed graph, and the force directed graph is a good choice to make a clean overview. It automatically draw attention to the characters of focus in terms of killing, e.g. Arya Stark, Sandor Clegane, Daenarys Targaryan, …. Moreover, it shows completely different structures around these “killers”. Sandor Clegane is the center of a circle of characters killed, but seldom going out further, as these are not main characters. Arya Stark, on the other hand, is the center of a much bigger and more complicated network, involved in one of the longest killing chains, with many main characters involved in vengeances. It is also easy to note the nodes with only an self-pointing arrow, corresponding to self-killing.

### Character Death and Killing in each house(Arc Diagram)
2.1 Visual encoding:
As an alternative to the directed graph for visualizing character death and killing in each house, arc diagram also encodes each character as a circle node and encodes the group of each character as the color of the node. For convenience of implementation, in arc diagram, the direction of killing (i.e. source and target) is encoded by the color of the arc instead of direction of arrow. For example, if node A killed node B, then the color of the arc should be the color of node A. However, if node A and node B come from the same group, color  encoding of the arc can still be confusing. We use mouseover to clarify possible confusion like this. Size of node is chosen so that the diagram can fit into the screen; collection of color is chosen so that all color are distinctive and clear. The vertical position of nodes encodes ranking of characters according to the selected order(name alphabet order, group alphabet order, number of killing) by users.

2.2 Interaction techniques:
The first interaction is the pull-down menu where user can select ranking standard. By choosing “order by name”, user can look up specific character easily; by choosing “order by group”, user can explore the death and killing of each group; by choosing “order by kill”, user can see which characters killed most people. The second interaction is the mouse hovering. When mouse is over a certain node C, the node C is bolded and other nodes who are killed by it or killed it is also displayed. Arcs that are red indicate node C killed these nodes; arcs that are black indicate node C is killed by these nodes.
 
2.3 Comparison of directed graph and arc diagram for visualizing character death and killing:
We think that these two graphs have their own advantages and can emphasize different sub aspects. Directed graph can fit all characters in a reasonable area and provides a quick overview to users as to which character/group killed the most people. User can drag clusters of nodes(i.e. characters) to explore the complicated relation of killing and being killed and even cooperation and enmity between groups. However, lookup of certain node and more detailed ranking of kills are difficult to do in this graph. Arc diagram provides easy lookup and ranking of nodes. Disadvantage of arc diagram is that it takes up too much area. Thus we provide combination of these two diagrams for thorough exploration of the dataset.

### Character Death Timeline(Scatter plot)
3.1 Visual encoding:
This graph serves as a general timeline of all the deaths of the major characters in Game of Thrones the TV series. The dimension we are the most concerned about in this graph is the time of occurrence of each deaths. Therefore we drew the time axis as the only axis in this graph and encoded the time as the x-coordinate of the points, which represent the occurrence of the deaths. This visual encoding enables viewers to read the time and time order of the death occurrences easily. The y-coordinate of the points encodes the order of the occurrence, which enables views to see the number of deaths happened in each season and each episode. Since curious reader may be also interested in the name of the character who died in certain episode, we encoded this information as a label next to the dots. For even more curious readers, we encoded the detail information such as the murderer, location, manner of the deaths in the tags which will appear when the reader hover his cursor onto the points.

3.2 Interaction techniques:
The two major interaction techniques are displaying death details by mouse hovering and switching between seasons with buttons.

3.3 The rationale:
The timeline of a story is like the backbone of a man - it is straight but it tells a lot. We figure if we want to tell a story, we’d better have a timeline. Also with this philosophy, we would like to get a design that is on the one hand simple and straight, on the other hand as informative as possible. For simplicity, we drew only the most important axis - the time axis and used points to denote the occurrence of events. This way, we think it is clear that the time is the most important information we want to convey. We also wanted the timeline to be informative. We figured that using a temporary floating message box for detailed information will do the job while keeping the graph clean. Also for the reason of the cleaness,  we splitted the timeline into 8 seasons, so that we won’t have to show all the 200+ deaths in the same graph. So far the color of the dots does not encode any information except that the black and red color is usually culturally linked to tragic events like loss and deaths. In the later version we might consider encoding the allegiance or sex as color if that reviews interesting information. The transition animation is designed so that it is clear to the readers whether they are travelling forward or backward in time.

### Character Death Timeline(Parallel coordinate plot)
	4.1 Visual encoding:
The dataset includes the character names,  allegiances, gender,  death year, and death in which     chapter of which book and if they are nobility e.t.c.To show multiple information at the same time, I think parallel coordinate is an appropriate choice. Each axis encodes a property of the death,  and each line path encodes the information of a character. The color encodes the gender of a character, red for female and blue for male.

	4.2 Interaction techniques:
Brushing with highlighted paths allows people to chose the data they are interested in, and somewhat shows distributions of the data. Dragging the axis makes the comparison easier to see. And the search function compensates for the drawback that the name axis can’t be brushed, though it’s not a good idea to brush the name. The search makes it possible to look up for characters that being cared about.	

  4.3 Alternative ways:
Can do the Timeline plot like the timeline for the TV shows, by showing the details when hovers above the point. In that way, it’s easier to see the time structure of the deaths, but makes it difficult to view  from other aspects. With the parallel coordinate plot, one can easily tell which Houses are focused on in which book, and how many people are dead for what Houses. Another thought is to delete the “Name” info, and do a counting of each selected brush, that will give more precise statistics, but we decide to keep the Name because it’s important to people to look up for particular character.

## Overview of design process
	Each of us worked on one visualization: 
- Zhengde Zhao: Directed graph. 15 hours.
- Yaxuan Zhou: arc diagram. 15hours
- Zijian Li: Scatter plot. 15 hours.
- Yue Zhao: parallel coordinate plot. 15hours.
	The preprocessing of data, customized design of visualization interface and debugging of errors took the most time.
