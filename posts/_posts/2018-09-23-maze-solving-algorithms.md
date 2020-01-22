---
title: Maze Solving Algorithms
image: /assets/img/posts/maze_runner.gif
description: >
  Maze Runner is a visualization tool for maze generation and path solving using JavaScript and HTML5 Canvas. It provides insight into the behavior of popular maze generation and traversal algorithms, such as Breadth-First Search (BFS), Depth-First Search (DFS), and A* Search.
---

Here is the experimental results of comparing different searching algorithm using the maze runner. In the following order, we have Breadth-First Search, Depth-First Search, and A* Search.

<img id="maze_thumbnail" src="https://i.gyazo.com/thumb/400/_8acddd2ae042291c5e9e51950f8afad5-gif.gif" alt="Maze that demonstrates AI capabilities" title="Maze solver"/>

<link rel="stylesheet" type="text/css" href="/assets/js/maze/maze.css">

<div style="text-align:center" id="maze_runner">
  <canvas id="runner1" width="350" height="425"></canvas>
  <canvas id="runner2" width="350" height="425"></canvas>
  <canvas id="runner3" width="350" height="425"></canvas>
  <p>
    <button class="buttonBlue" id="restart">Restart</button> 
    <button class="buttonBlue" id="reset">New maze</button>
  </p>
</div>
<p>This game was written in Javascript.</p>	

<script>
  var elementExists = document.getElementsByClassName("read-more");
  
  var mazer_runner = document.getElementById("maze_runner");
  var maze_thumbnail = document.getElementById("maze_thumbnail");

  if (elementExists.length === 0) {
    mazer_runner.style.display = "block";
    maze_thumbnail.style.display = "none";
  } else {
    mazer_runner.style.display = "none";
    maze_thumbnail.style.display = "block";
  }
</script>

<script src="/assets/js/maze/buckets.min.js"></script>
<script src="/assets/js/maze/cell.js"></script>

# Let's discuss those results:  

## Breadth-First Search

BFS is a search algorithm for traversing a graph or tree. It starts by visiting a node, then adds all of that node's neighbors into the queue. Each time it adds a neighbor to the queue, it adds a pointer that references the neighboring node's parent. Once the queue is empty, which means all nodes have been visited, or the goal node is found (for early-exit implementations), the pointers are traced from the goal back to the source.

## Depth-First Search 

DFS is a search algorithm for traversing a graph or tree. Rather than considering its shallow neighbors first like BFS, it plunges all the way to the bottom of a given branch before considering the next neighbor. Once the stack is empty, which means all nodes have been visited, or the goal node is found (for early-exit implementations), the pointers are traced from the goal back to the source.

## A* Search

Unlike BFS and DFS, A* is an informed search algorithm. A* is implemented by searching the possible paths to the goal and opting for the one that incurs the smallest cost. The cost used by A* is the actual distance incremented from the start to the current node plus the estimated distance to the goal. To determine the cost to the goal, there are a number of heuristics. Two popular options are Manhattan distance and straight-line distance. In the Manhattan heuristic, the distance to the goal in the vertical direction plus the distance to the goal in the horizontal direction. While in the straight-line heuristic, the straight-line distance to the goal is used as the estimate.

[You can find the code for this article on GitHub](https://github.com/andk123/Maze-Solving-Traversal-Algorithms)