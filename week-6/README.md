# Week 6: Graph Basics (DFS/BFS) - Daily Structured Plan

## 📅 **DAY 1: Graph Fundamentals & Representations**

### 🌅 **Morning Session (45 minutes)**
#### Understanding Graphs
- **Core Concepts:**
  - Graph terminology (vertices, edges, directed/undirected)
  - Connected components
  - Cycles and acyclic graphs
  - Weighted vs unweighted graphs
  - Graph vs Tree differences

#### Graph Representations:
```java
// Different ways to represent graphs
class GraphRepresentations {
    
    // 1. Adjacency Matrix
    class GraphMatrix {
        private int[][] adjMatrix;
        private int numVertices;
        
        public GraphMatrix(int numVertices) {
            this.numVertices = numVertices;
            adjMatrix = new int[numVertices][numVertices];
        }
        
        // Add edge (undirected)
        public void addEdge(int src, int dest) {
            adjMatrix[src][dest] = 1;
            adjMatrix[dest][src] = 1; // Remove for directed graph
        }
        
        // Add weighted edge
        public void addWeightedEdge(int src, int dest, int weight) {
            adjMatrix[src][dest] = weight;
            adjMatrix[dest][src] = weight; // Remove for directed
        }
        
        // Check if edge exists
        public boolean hasEdge(int src, int dest) {
            return adjMatrix[src][dest] != 0;
        }
        
        // Get neighbors
        public List<Integer> getNeighbors(int vertex) {
            List<Integer> neighbors = new ArrayList<>();
            for (int i = 0; i < numVertices; i++) {
                if (adjMatrix[vertex][i] != 0) {
                    neighbors.add(i);
                }
            }
            return neighbors;
        }
    }
    
    // 2. Adjacency List (Most Common)
    class GraphList {
        private Map<Integer, List<Integer>> adjList;
        private int numVertices;
        
        public GraphList(int numVertices) {
            this.numVertices = numVertices;
            adjList = new HashMap<>();
            for (int i = 0; i < numVertices; i++) {
                adjList.put(i, new ArrayList<>());
            }
        }
        
        // Add edge (undirected)
        public void addEdge(int src, int dest) {
            adjList.get(src).add(dest);
            adjList.get(dest).add(src); // Remove for directed
        }
        
        // Get neighbors
        public List<Integer> getNeighbors(int vertex) {
            return adjList.getOrDefault(vertex, new ArrayList<>());
        }
        
        // Print graph
        public void printGraph() {
            for (int vertex : adjList.keySet()) {
                System.out.print(vertex + " -> ");
                for (int neighbor : adjList.get(vertex)) {
                    System.out.print(neighbor + " ");
                }
                System.out.println();
            }
        }
    }
    
    // 3. Edge List
    class Edge {
        int src, dest, weight;
        
        Edge(int src, int dest, int weight) {
            this.src = src;
            this.dest = dest;
            this.weight = weight;
        }
    }
    
    class GraphEdgeList {
        private List<Edge> edges;
        private int numVertices;
        
        public GraphEdgeList(int numVertices) {
            this.numVertices = numVertices;
            edges = new ArrayList<>();
        }
        
        public void addEdge(int src, int dest, int weight) {
            edges.add(new Edge(src, dest, weight));
        }
        
        // Convert to adjacency list
        public Map<Integer, List<int[]>> toAdjList() {
            Map<Integer, List<int[]>> adjList = new HashMap<>();
            
            for (Edge edge : edges) {
                adjList.computeIfAbsent(edge.src, k -> new ArrayList<>())
                       .add(new int[]{edge.dest, edge.weight});
            }
            
            return adjList;
        }
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Building Graphs from Problems
```java
class GraphBuilder {
    // Build graph from edges array
    public Map<Integer, List<Integer>> buildGraph(int[][] edges, int n) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        
        // Initialize all vertices
        for (int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        // Add edges
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]); // Remove for directed
        }
        
        return graph;
    }
    
    // Build graph from prerequisites (directed)
    public Map<Integer, List<Integer>> buildDigraph(int[][] prerequisites, int n) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        
        for (int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (int[] prereq : prerequisites) {
            graph.get(prereq[1]).add(prereq[0]); // prereq[1] -> prereq[0]
        }
        
        return graph;
    }
    
    // Grid as graph (implicit representation)
    class GridGraph {
        private int[][] grid;
        private int rows, cols;
        
        // 4 directions: up, right, down, left
        private int[][] directions = {{-1,0}, {0,1}, {1,0}, {0,-1}};
        
        // 8 directions (including diagonals)
        private int[][] directions8 = {
            {-1,-1}, {-1,0}, {-1,1},
            {0,-1},           {0,1},
            {1,-1},  {1,0},   {1,1}
        };
        
        public GridGraph(int[][] grid) {
            this.grid = grid;
            this.rows = grid.length;
            this.cols = grid[0].length;
        }
        
        // Get valid neighbors for cell (i, j)
        public List<int[]> getNeighbors(int i, int j) {
            List<int[]> neighbors = new ArrayList<>();
            
            for (int[] dir : directions) {
                int newI = i + dir[0];
                int newJ = j + dir[1];
                
                if (isValid(newI, newJ)) {
                    neighbors.add(new int[]{newI, newJ});
                }
            }
            
            return neighbors;
        }
        
        private boolean isValid(int i, int j) {
            return i >= 0 && i < rows && j >= 0 && j < cols;
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Graph Properties and Basic Operations
```java
class GraphProperties {
    // Count vertices and edges
    public void graphStats(Map<Integer, List<Integer>> graph) {
        int vertices = graph.size();
        int edges = 0;
        
        for (List<Integer> neighbors : graph.values()) {
            edges += neighbors.size();
        }
        
        // For undirected graph, each edge counted twice
        edges = edges / 2;
        
        System.out.println("Vertices: " + vertices);
        System.out.println("Edges: " + edges);
    }
    
    // Degree of vertices
    public Map<Integer, Integer> calculateDegrees(Map<Integer, List<Integer>> graph) {
        Map<Integer, Integer> degrees = new HashMap<>();
        
        for (Map.Entry<Integer, List<Integer>> entry : graph.entrySet()) {
            degrees.put(entry.getKey(), entry.getValue().size());
        }
        
        return degrees;
    }
    
    // Check if graph is complete
    public boolean isComplete(Map<Integer, List<Integer>> graph) {
        int n = graph.size();
        
        for (List<Integer> neighbors : graph.values()) {
            if (neighbors.size() != n - 1) {
                return false;
            }
        }
        
        return true;
    }
}
```

### 📝 **Day 1 Checklist**
- [ ] Understand graph terminology
- [ ] Master adjacency list representation
- [ ] Learn adjacency matrix pros/cons
- [ ] Convert between representations
- [ ] Build graphs from problem inputs

---

## 📅 **DAY 2: DFS on Graphs**

### 🌅 **Morning Session (45 minutes)**
#### DFS Implementation and Applications
```java
class GraphDFS {
    // Basic DFS traversal
    public void dfsTraversal(Map<Integer, List<Integer>> graph, int start) {
        Set<Integer> visited = new HashSet<>();
        dfsHelper(graph, start, visited);
    }
    
    private void dfsHelper(Map<Integer, List<Integer>> graph, int node, 
                          Set<Integer> visited) {
        visited.add(node);
        System.out.print(node + " ");
        
        for (int neighbor : graph.get(node)) {
            if (!visited.contains(neighbor)) {
                dfsHelper(graph, neighbor, visited);
            }
        }
    }
    
    // DFS to find all connected components
    public List<List<Integer>> findConnectedComponents(Map<Integer, List<Integer>> graph) {
        List<List<Integer>> components = new ArrayList<>();
        Set<Integer> visited = new HashSet<>();
        
        for (int node : graph.keySet()) {
            if (!visited.contains(node)) {
                List<Integer> component = new ArrayList<>();
                dfsComponent(graph, node, visited, component);
                components.add(component);
            }
        }
        
        return components;
    }
    
    private void dfsComponent(Map<Integer, List<Integer>> graph, int node,
                             Set<Integer> visited, List<Integer> component) {
        visited.add(node);
        component.add(node);
        
        for (int neighbor : graph.get(node)) {
            if (!visited.contains(neighbor)) {
                dfsComponent(graph, neighbor, visited, component);
            }
        }
    }
    
    // DFS to check if path exists
    public boolean hasPath(Map<Integer, List<Integer>> graph, int start, int end) {
        if (start == end) return true;
        
        Set<Integer> visited = new HashSet<>();
        return dfsPath(graph, start, end, visited);
    }
    
    private boolean dfsPath(Map<Integer, List<Integer>> graph, int current, 
                           int end, Set<Integer> visited) {
        if (current == end) return true;
        
        visited.add(current);
        
        for (int neighbor : graph.get(current)) {
            if (!visited.contains(neighbor)) {
                if (dfsPath(graph, neighbor, end, visited)) {
                    return true;
                }
            }
        }
        
        return false;
    }
    
    // Find all paths from source to target
    public List<List<Integer>> allPaths(Map<Integer, List<Integer>> graph, 
                                        int source, int target) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> path = new ArrayList<>();
        path.add(source);
        dfsAllPaths(graph, source, target, path, result);
        return result;
    }
    
    private void dfsAllPaths(Map<Integer, List<Integer>> graph, int current, 
                            int target, List<Integer> path, 
                            List<List<Integer>> result) {
        if (current == target) {
            result.add(new ArrayList<>(path));
            return;
        }
        
        for (int neighbor : graph.get(current)) {
            // For DAG, no need to track visited
            // For graph with cycles, need visited set
            path.add(neighbor);
            dfsAllPaths(graph, neighbor, target, path, result);
            path.remove(path.size() - 1); // backtrack
        }
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### DFS on Grid (2D Array as Graph)
```java
class GridDFS {
    private int[][] directions = {{-1,0}, {0,1}, {1,0}, {0,-1}};
    
    // Number of Islands
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) return 0;
        
        int rows = grid.length;
        int cols = grid[0].length;
        int islands = 0;
        
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == '1') {
                    islands++;
                    dfsIsland(grid, i, j);
                }
            }
        }
        
        return islands;
    }
    
    private void dfsIsland(char[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length 
            || grid[i][j] == '0') {
            return;
        }
        
        grid[i][j] = '0'; // Mark as visited
        
        for (int[] dir : directions) {
            dfsIsland(grid, i + dir[0], j + dir[1]);
        }
    }
    
    // Max Area of Island
    public int maxAreaOfIsland(int[][] grid) {
        int maxArea = 0;
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    maxArea = Math.max(maxArea, dfsArea(grid, i, j));
                }
            }
        }
        
        return maxArea;
    }
    
    private int dfsArea(int[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length 
            || grid[i][j] == 0) {
            return 0;
        }
        
        grid[i][j] = 0; // Mark as visited
        int area = 1;
        
        for (int[] dir : directions) {
            area += dfsArea(grid, i + dir[0], j + dir[1]);
        }
        
        return area;
    }
    
    // Flood Fill
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int originalColor = image[sr][sc];
        if (originalColor == newColor) return image;
        
        dfsFlood(image, sr, sc, originalColor, newColor);
        return image;
    }
    
    private void dfsFlood(int[][] image, int i, int j, int oldColor, int newColor) {
        if (i < 0 || i >= image.length || j < 0 || j >= image[0].length 
            || image[i][j] != oldColor) {
            return;
        }
        
        image[i][j] = newColor;
        
        for (int[] dir : directions) {
            dfsFlood(image, i + dir[0], j + dir[1], oldColor, newColor);
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
- **Then:** [733. Flood Fill](https://leetcode.com/problems/flood-fill/)

### 📝 **Day 2 Checklist**
- [ ] Implement DFS traversal recursively
- [ ] Find connected components using DFS
- [ ] Master DFS on 2D grids
- [ ] Complete Number of Islands
- [ ] Solve Flood Fill problem

---

## 📅 **DAY 3: BFS on Graphs**

### 🌅 **Morning Session (45 minutes)**
#### BFS Implementation and Applications
```java
class GraphBFS {
    // Basic BFS traversal
    public void bfsTraversal(Map<Integer, List<Integer>> graph, int start) {
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();
        
        visited.add(start);
        queue.offer(start);
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            
            for (int neighbor : graph.get(node)) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
    }
    
    // BFS for shortest path (unweighted graph)
    public int shortestPath(Map<Integer, List<Integer>> graph, int start, int end) {
        if (start == end) return 0;
        
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();
        
        visited.add(start);
        queue.offer(start);
        int distance = 0;
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            distance++;
            
            for (int i = 0; i < size; i++) {
                int node = queue.poll();
                
                for (int neighbor : graph.get(node)) {
                    if (neighbor == end) return distance;
                    
                    if (!visited.contains(neighbor)) {
                        visited.add(neighbor);
                        queue.offer(neighbor);
                    }
                }
            }
        }
        
        return -1; // No path found
    }
    
    // BFS to find shortest path with parent tracking
    public List<Integer> shortestPathNodes(Map<Integer, List<Integer>> graph, 
                                           int start, int end) {
        Map<Integer, Integer> parent = new HashMap<>();
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        
        visited.add(start);
        queue.offer(start);
        parent.put(start, null);
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            
            if (node == end) {
                return reconstructPath(parent, end);
            }
            
            for (int neighbor : graph.get(node)) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    parent.put(neighbor, node);
                    queue.offer(neighbor);
                }
            }
        }
        
        return new ArrayList<>(); // No path
    }
    
    private List<Integer> reconstructPath(Map<Integer, Integer> parent, int end) {
        List<Integer> path = new ArrayList<>();
        Integer current = end;
        
        while (current != null) {
            path.add(0, current); // Add to front
            current = parent.get(current);
        }
        
        return path;
    }
    
    // Level order traversal of graph
    public List<List<Integer>> levelOrder(Map<Integer, List<Integer>> graph, int start) {
        List<List<Integer>> levels = new ArrayList<>();
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();
        
        visited.add(start);
        queue.offer(start);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> currentLevel = new ArrayList<>();
            
            for (int i = 0; i < size; i++) {
                int node = queue.poll();
                currentLevel.add(node);
                
                for (int neighbor : graph.get(node)) {
                    if (!visited.contains(neighbor)) {
                        visited.add(neighbor);
                        queue.offer(neighbor);
                    }
                }
            }
            
            levels.add(currentLevel);
        }
        
        return levels;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### BFS on Grid and Multi-Source BFS
```java
class GridBFS {
    private int[][] directions = {{-1,0}, {0,1}, {1,0}, {0,-1}};
    
    // Shortest path in binary matrix
    public int shortestPathBinaryMatrix(int[][] grid) {
        int n = grid.length;
        
        if (grid[0][0] == 1 || grid[n-1][n-1] == 1) return -1;
        
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{0, 0});
        grid[0][0] = 1; // Mark as visited with distance
        
        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            int row = cell[0], col = cell[1];
            int distance = grid[row][col];
            
            if (row == n-1 && col == n-1) {
                return distance;
            }
            
            // 8 directions for this problem
            int[][] dirs = {{-1,-1},{-1,0},{-1,1},{0,-1},{0,1},{1,-1},{1,0},{1,1}};
            
            for (int[] dir : dirs) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];
                
                if (newRow >= 0 && newRow < n && newCol >= 0 && newCol < n 
                    && grid[newRow][newCol] == 0) {
                    queue.offer(new int[]{newRow, newCol});
                    grid[newRow][newCol] = distance + 1;
                }
            }
        }
        
        return -1;
    }
    
    // Rotting Oranges (Multi-source BFS)
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        Queue<int[]> queue = new LinkedList<>();
        int freshCount = 0;
        
        // Find all rotten oranges and count fresh ones
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }
        
        if (freshCount == 0) return 0;
        
        int minutes = -1;
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            minutes++;
            
            for (int i = 0; i < size; i++) {
                int[] cell = queue.poll();
                
                for (int[] dir : directions) {
                    int newRow = cell[0] + dir[0];
                    int newCol = cell[1] + dir[1];
                    
                    if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols 
                        && grid[newRow][newCol] == 1) {
                        grid[newRow][newCol] = 2;
                        freshCount--;
                        queue.offer(new int[]{newRow, newCol});
                    }
                }
            }
        }
        
        return freshCount == 0 ? minutes : -1;
    }
    
    // Walls and Gates (Multi-source BFS)
    public void wallsAndGates(int[][] rooms) {
        int INF = 2147483647;
        int rows = rooms.length;
        int cols = rooms[0].length;
        Queue<int[]> queue = new LinkedList<>();
        
        // Add all gates to queue
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (rooms[i][j] == 0) {
                    queue.offer(new int[]{i, j});
                }
            }
        }
        
        // BFS from all gates simultaneously
        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            int row = cell[0], col = cell[1];
            
            for (int[] dir : directions) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];
                
                if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols 
                    && rooms[newRow][newCol] == INF) {
                    rooms[newRow][newCol] = rooms[row][col] + 1;
                    queue.offer(new int[]{newRow, newCol});
                }
            }
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
- **Then:** [1091. Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

### 📝 **Day 3 Checklist**
- [ ] Implement BFS with queue
- [ ] Find shortest path using BFS
- [ ] Master multi-source BFS
- [ ] Complete Rotting Oranges
- [ ] Solve shortest path in matrix

---

## 📅 **DAY 4: Cycle Detection**

### 🌅 **Morning Session (45 minutes)**
#### Cycle Detection in Different Graph Types
```java
class CycleDetection {
    // Cycle detection in undirected graph using DFS
    public boolean hasCycleUndirectedDFS(Map<Integer, List<Integer>> graph) {
        Set<Integer> visited = new HashSet<>();
        
        for (int node : graph.keySet()) {
            if (!visited.contains(node)) {
                if (dfsCycleUndirected(graph, node, -1, visited)) {
                    return true;
                }
            }
        }
        
        return false;
    }
    
    private boolean dfsCycleUndirected(Map<Integer, List<Integer>> graph, 
                                      int node, int parent, Set<Integer> visited) {
        visited.add(node);
        
        for (int neighbor : graph.get(node)) {
            if (!visited.contains(neighbor)) {
                if (dfsCycleUndirected(graph, neighbor, node, visited)) {
                    return true;
                }
            } else if (neighbor != parent) {
                return true; // Back edge found
            }
        }
        
        return false;
    }
    
    // Cycle detection in directed graph using DFS (3 colors)
    public boolean hasCycleDirectedDFS(Map<Integer, List<Integer>> graph) {
        Map<Integer, Integer> color = new HashMap<>();
        // 0 = white (unvisited), 1 = gray (visiting), 2 = black (visited)
        
        for (int node : graph.keySet()) {
            color.put(node, 0);
        }
        
        for (int node : graph.keySet()) {
            if (color.get(node) == 0) {
                if (dfsCycleDirected(graph, node, color)) {
                    return true;
                }
            }
        }
        
        return false;
    }
    
    private boolean dfsCycleDirected(Map<Integer, List<Integer>> graph, 
                                    int node, Map<Integer, Integer> color) {
        color.put(node, 1); // Mark as gray (visiting)
        
        for (int neighbor : graph.get(node)) {
            if (color.get(neighbor) == 1) {
                return true; // Back edge to gray node = cycle
            }
            if (color.get(neighbor) == 0) {
                if (dfsCycleDirected(graph, neighbor, color)) {
                    return true;
                }
            }
        }
        
        color.put(node, 2); // Mark as black (visited)
        return false;
    }
    
    // Course Schedule (Cycle detection application)
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // Build graph
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (int[] prereq : prerequisites) {
            graph.get(prereq[1]).add(prereq[0]);
        }
        
        // Check for cycle
        return !hasCycleDirectedDFS(graph);
    }
    
    // Find cycle in directed graph and return nodes in cycle
    public List<Integer> findCycle(Map<Integer, List<Integer>> graph) {
        Map<Integer, Integer> state = new HashMap<>();
        Map<Integer, Integer> parent = new HashMap<>();
        List<Integer> cycle = new ArrayList<>();
        
        for (int node : graph.keySet()) {
            state.put(node, 0); // white
            parent.put(node, -1);
        }
        
        for (int node : graph.keySet()) {
            if (state.get(node) == 0) {
                if (dfsFindCycle(graph, node, state, parent, cycle)) {
                    return cycle;
                }
            }
        }
        
        return cycle;
    }
    
    private boolean dfsFindCycle(Map<Integer, List<Integer>> graph, int node,
                                Map<Integer, Integer> state, Map<Integer, Integer> parent,
                                List<Integer> cycle) {
        state.put(node, 1); // gray
        
        for (int neighbor : graph.get(node)) {
            parent.put(neighbor, node);
            
            if (state.get(neighbor) == 1) {
                // Found cycle, reconstruct it
                int curr = node;
                while (curr != neighbor) {
                    cycle.add(0, curr);
                    curr = parent.get(curr);
                }
                cycle.add(0, neighbor);
                return true;
            }
            
            if (state.get(neighbor) == 0) {
                if (dfsFindCycle(graph, neighbor, state, parent, cycle)) {
                    return true;
                }
            }
        }
        
        state.put(node, 2); // black
        return false;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Cycle Detection using BFS (Kahn's Algorithm)
```java
class CycleDetectionBFS {
    // Topological sort using BFS (Kahn's algorithm)
    public boolean canFinishBFS(int numCourses, int[][] prerequisites) {
        // Build graph and calculate indegrees
        Map<Integer, List<Integer>> graph = new HashMap<>();
        int[] indegree = new int[numCourses];
        
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (int[] prereq : prerequisites) {
            graph.get(prereq[1]).add(prereq[0]);
            indegree[prereq[0]]++;
        }
        
        // BFS with nodes having 0 indegree
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }
        
        int processedCourses = 0;
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            processedCourses++;
            
            for (int neighbor : graph.get(course)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        
        return processedCourses == numCourses;
    }
    
    // Get topological order
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        int[] indegree = new int[numCourses];
        
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (int[] prereq : prerequisites) {
            graph.get(prereq[1]).add(prereq[0]);
            indegree[prereq[0]]++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }
        
        int[] order = new int[numCourses];
        int index = 0;
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            order[index++] = course;
            
            for (int neighbor : graph.get(course)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        
        return index == numCourses ? order : new int[0];
    }
    
    // Alien Dictionary (Topological sort application)
    public String alienOrder(String[] words) {
        // Build graph
        Map<Character, Set<Character>> graph = new HashMap<>();
        Map<Character, Integer> indegree = new HashMap<>();
        
        // Initialize all characters
        for (String word : words) {
            for (char c : word.toCharArray()) {
                graph.putIfAbsent(c, new HashSet<>());
                indegree.putIfAbsent(c, 0);
            }
        }
        
        // Build edges
        for (int i = 0; i < words.length - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];
            
            // Check invalid order
            if (word1.length() > word2.length() && word1.startsWith(word2)) {
                return "";
            }
            
            // Find first different character
            for (int j = 0; j < Math.min(word1.length(), word2.length()); j++) {
                char c1 = word1.charAt(j);
                char c2 = word2.charAt(j);
                
                if (c1 != c2) {
                    if (!graph.get(c1).contains(c2)) {
                        graph.get(c1).add(c2);
                        indegree.put(c2, indegree.get(c2) + 1);
                    }
                    break;
                }
            }
        }
        
        // Topological sort
        Queue<Character> queue = new LinkedList<>();
        for (char c : indegree.keySet()) {
            if (indegree.get(c) == 0) {
                queue.offer(c);
            }
        }
        
        StringBuilder result = new StringBuilder();
        while (!queue.isEmpty()) {
            char c = queue.poll();
            result.append(c);
            
            for (char neighbor : graph.get(c)) {
                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        
        return result.length() == indegree.size() ? result.toString() : "";
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
- **Then:** [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

### 📝 **Day 4 Checklist**
- [ ] Understand cycle detection in directed vs undirected
- [ ] Implement DFS three-color algorithm
- [ ] Master Kahn's algorithm (BFS topological sort)
- [ ] Complete Course Schedule I
- [ ] Solve Course Schedule II

---

## 📅 **DAY 5: Graph Coloring and Bipartite**

### 🌅 **Morning Session (45 minutes)**
#### Bipartite Graph Detection
```java
class BipartiteGraph {
    // Check if graph is bipartite using BFS
    public boolean isBipartiteBFS(int[][] graph) {
        int n = graph.length;
        int[] colors = new int[n];
        Arrays.fill(colors, -1);
        
        for (int i = 0; i < n; i++) {
            if (colors[i] == -1) {
                if (!bfsBipartite(graph, i, colors)) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
    private boolean bfsBipartite(int[][] graph, int start, int[] colors) {
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start);
        colors[start] = 0;
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            
            for (int neighbor : graph[node]) {
                if (colors[neighbor] == -1) {
                    colors[neighbor] = 1 - colors[node];
                    queue.offer(neighbor);
                } else if (colors[neighbor] == colors[node]) {
                    return false; // Same color as neighbor
                }
            }
        }
        
        return true;
    }
    
    // Check if bipartite using DFS
    public boolean isBipartiteDFS(int[][] graph) {
        int n = graph.length;
        int[] colors = new int[n];
        Arrays.fill(colors, -1);
        
        for (int i = 0; i < n; i++) {
            if (colors[i] == -1) {
                if (!dfsBipartite(graph, i, 0, colors)) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
    private boolean dfsBipartite(int[][] graph, int node, int color, int[] colors) {
        colors[node] = color;
        
        for (int neighbor : graph[node]) {
            if (colors[neighbor] == -1) {
                if (!dfsBipartite(graph, neighbor, 1 - color, colors)) {
                    return false;
                }
            } else if (colors[neighbor] == color) {
                return false;
            }
        }
        
        return true;
    }
    
    // Possible Bipartition
    public boolean possibleBipartition(int n, int[][] dislikes) {
        // Build graph
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 1; i <= n; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (int[] dislike : dislikes) {
            graph.get(dislike[0]).add(dislike[1]);
            graph.get(dislike[1]).add(dislike[0]);
        }
        
        // Check if bipartite
        Map<Integer, Integer> colors = new HashMap<>();
        
        for (int i = 1; i <= n; i++) {
            if (!colors.containsKey(i)) {
                if (!dfsColor(graph, i, 0, colors)) {
                    return false;
                }
            }
        }
        
        return true;
    }
    
    private boolean dfsColor(Map<Integer, List<Integer>> graph, int node, 
                            int color, Map<Integer, Integer> colors) {
        colors.put(node, color);
        
        for (int neighbor : graph.get(node)) {
            if (!colors.containsKey(neighbor)) {
                if (!dfsColor(graph, neighbor, 1 - color, colors)) {
                    return false;
                }
            } else if (colors.get(neighbor) == color) {
                return false;
            }
        }
        
        return true;
    }
}
```

### 🌞 **Afternoon Session (45 minutes)**
#### Graph Coloring Problems
```java
class GraphColoring {
    // M-coloring problem (backtracking)
    public boolean graphColoring(int[][] graph, int m, int n) {
        int[] colors = new int[n];
        return canColor(graph, m, colors, 0);
    }
    
    private boolean canColor(int[][] graph, int m, int[] colors, int node) {
        if (node == graph.length) {
            return true; // All nodes colored
        }
        
        for (int color = 1; color <= m; color++) {
            if (isSafeColor(graph, colors, node, color)) {
                colors[node] = color;
                
                if (canColor(graph, m, colors, node + 1)) {
                    return true;
                }
                
                colors[node] = 0; // Backtrack
            }
        }
        
        return false;
    }
    
    private boolean isSafeColor(int[][] graph, int[] colors, int node, int color) {
        for (int i = 0; i < graph.length; i++) {
            if (graph[node][i] == 1 && colors[i] == color) {
                return false;
            }
        }
        return true;
    }
    
    // Flower Planting (4-coloring specific)
    public int[] gardenNoAdj(int n, int[][] paths) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        
        for (int i = 1; i <= n; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (int[] path : paths) {
            graph.get(path[0]).add(path[1]);
            graph.get(path[1]).add(path[0]);
        }
        
        int[] colors = new int[n];
        
        for (int i = 1; i <= n; i++) {
            Set<Integer> usedColors = new HashSet<>();
            
            for (int neighbor : graph.get(i)) {
                if (neighbor < i) { // Already colored
                    usedColors.add(colors[neighbor - 1]);
                }
            }
            
            // Assign first available color
            for (int color = 1; color <= 4; color++) {
                if (!usedColors.contains(color)) {
                    colors[i - 1] = color;
                    break;
                }
            }
        }
        
        return colors;
    }
    
    // Is Graph Bipartite (2-coloring)
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] colors = new int[n];
        
        for (int i = 0; i < n; i++) {
            if (colors[i] == 0) {
                Queue<Integer> queue = new LinkedList<>();
                queue.offer(i);
                colors[i] = 1;
                
                while (!queue.isEmpty()) {
                    int node = queue.poll();
                    
                    for (int neighbor : graph[node]) {
                        if (colors[neighbor] == 0) {
                            colors[neighbor] = -colors[node];
                            queue.offer(neighbor);
                        } else if (colors[neighbor] == colors[node]) {
                            return false;
                        }
                    }
                }
            }
        }
        
        return true;
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### LeetCode Practice
- **Solve:** [785. Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)
- **Then:** [886. Possible Bipartition](https://leetcode.com/problems/possible-bipartition/)

### 📝 **Day 5 Checklist**
- [ ] Understand bipartite graph properties
- [ ] Implement bipartite checking (BFS/DFS)
- [ ] Learn graph coloring basics
- [ ] Complete Is Graph Bipartite
- [ ] Solve Possible Bipartition

---

## 📅 **DAY 6: Practice & Complex Graph Problems**

### 🌅 **Morning Session (60 minutes)**
#### Clone and Transform Graph Problems
```java
class GraphTransform {
    // Clone Graph
    class Node {
        public int val;
        public List<Node> neighbors;
        
        public Node() {
            val = 0;
            neighbors = new ArrayList<>();
        }
        
        public Node(int _val) {
            val = _val;
            neighbors = new ArrayList<>();
        }
    }
    
    // Clone Graph using DFS
    public Node cloneGraph(Node node) {
        if (node == null) return null;
        
        Map<Node, Node> visited = new HashMap<>();
        return cloneDFS(node, visited);
    }
    
    private Node cloneDFS(Node node, Map<Node, Node> visited) {
        if (visited.containsKey(node)) {
            return visited.get(node);
        }
        
        Node clone = new Node(node.val);
        visited.put(node, clone);
        
        for (Node neighbor : node.neighbors) {
            clone.neighbors.add(cloneDFS(neighbor, visited));
        }
        
        return clone;
    }
    
    // Clone Graph using BFS
    public Node cloneGraphBFS(Node node) {
        if (node == null) return null;
        
        Map<Node, Node> visited = new HashMap<>();
        Queue<Node> queue = new LinkedList<>();
        
        visited.put(node, new Node(node.val));
        queue.offer(node);
        
        while (!queue.isEmpty()) {
            Node current = queue.poll();
            
            for (Node neighbor : current.neighbors) {
                if (!visited.containsKey(neighbor)) {
                    visited.put(neighbor, new Node(neighbor.val));
                    queue.offer(neighbor);
                }
                visited.get(current).neighbors.add(visited.get(neighbor));
            }
        }
        
        return visited.get(node);
    }
    
    // Pacific Atlantic Water Flow
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        List<List<Integer>> result = new ArrayList<>();
        if (heights == null || heights.length == 0) return result;
        
        int rows = heights.length;
        int cols = heights[0].length;
        
        boolean[][] pacific = new boolean[rows][cols];
        boolean[][] atlantic = new boolean[rows][cols];
        
        // DFS from borders
        for (int i = 0; i < rows; i++) {
            dfsWater(heights, pacific, i, 0, Integer.MIN_VALUE);
            dfsWater(heights, atlantic, i, cols - 1, Integer.MIN_VALUE);
        }
        
        for (int j = 0; j < cols; j++) {
            dfsWater(heights, pacific, 0, j, Integer.MIN_VALUE);
            dfsWater(heights, atlantic, rows - 1, j, Integer.MIN_VALUE);
        }
        
        // Find cells that can reach both oceans
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (pacific[i][j] && atlantic[i][j]) {
                    result.add(Arrays.asList(i, j));
                }
            }
        }
        
        return result;
    }
    
    private void dfsWater(int[][] heights, boolean[][] visited, 
                         int i, int j, int prevHeight) {
        if (i < 0 || i >= heights.length || j < 0 || j >= heights[0].length
            || visited[i][j] || heights[i][j] < prevHeight) {
            return;
        }
        
        visited[i][j] = true;
        
        int[][] directions = {{-1,0}, {0,1}, {1,0}, {0,-1}};
        for (int[] dir : directions) {
            dfsWater(heights, visited, i + dir[0], j + dir[1], heights[i][j]);
        }
    }
}
```

### 🌞 **Afternoon Session (90 minutes)**
#### Problem-Solving Marathon
**Solve these problems independently:**

```java
// 1. Surrounded Regions
public void solve(char[][] board) {
    // Your implementation
    // Mark 'O's connected to border, then flip remaining 'O's
}

// 2. Word Search
public boolean exist(char[][] board, String word) {
    // Your implementation
    // DFS with backtracking
}

// 3. Keys and Rooms
public boolean canVisitAllRooms(List<List<Integer>> rooms) {
    // Your implementation
    // Simple DFS/BFS from room 0
}

// 4. Minimum Height Trees
public List<Integer> findMinHeightTrees(int n, int[][] edges) {
    // Your implementation
    // Hint: Remove leaves layer by layer
}
```

### 🌙 **Evening Session (45 minutes)**
#### LeetCode Challenge Set
- **Complete:**
  1. [133. Clone Graph](https://leetcode.com/problems/clone-graph/)
  2. [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)
  3. [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)

### 📝 **Day 6 Checklist**
- [ ] Master graph cloning techniques
- [ ] Solve water flow problem
- [ ] Complete surrounded regions
- [ ] Practice mixed difficulty problems
- [ ] Identify weak areas for review

---

## 📅 **DAY 7: Week Review & Advanced Applications**

### 🌅 **Morning Session (60 minutes)**
#### Comprehensive Review & Assessment
```java
// GRAPH MASTERY ASSESSMENT

/*
1. Time & Space Complexity:
- DFS: Time O(?), Space O(?)
- BFS: Time O(?), Space O(?)
- Topological Sort: Time O(?), Space O(?)
- Finding connected components: Time O(?)
- Cycle detection: Time O(?)

2. Choose the right approach:
Problem: Find shortest path in unweighted graph
a) DFS  b) BFS  c) Dijkstra  d) Bellman-Ford

Problem: Detect cycle in directed graph
a) BFS  b) DFS with colors  c) Union-Find  d) Topological Sort

Problem: Find all paths from source to target
a) BFS  b) DFS with backtracking  c) Dynamic Programming  d) Greedy

3. Debug this code:
*/
public boolean validPath(int n, int[][] edges, int start, int end) {
    Map<Integer, List<Integer>> graph = new HashMap<>();
    for (int[] edge : edges) {
        graph.get(edge[0]).add(edge[1]);  // Bug?
        graph.get(edge[1]).add(edge[0]);
    }
    
    Set<Integer> visited = new HashSet<>();
    return dfs(graph, start, end, visited);
}

private boolean dfs(Map<Integer, List<Integer>> graph, 
                   int current, int end, Set<Integer> visited) {
    if (current == end) return true;
    visited.add(current);
    
    for (int neighbor : graph.get(current)) {  // Bug?
        if (!visited.contains(neighbor)) {
            dfs(graph, neighbor, end, visited);  // Bug?
        }
    }
    return false;
}

/*
4. Graph vs Tree:
List 3 key differences between graphs and trees

5. When to use which traversal:
- Use DFS when: ?
- Use BFS when: ?
*/
```

### 🌞 **Afternoon Session (90 minutes)**
#### Advanced Graph Algorithms Preview
```java
class AdvancedGraphConcepts {
    // Union-Find (Disjoint Set) - Preview
    class UnionFind {
        private int[] parent;
        private int[] rank;
        
        public UnionFind(int n) {
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }
        
        public int find(int x) {
            if (parent[x] != x) {
                parent[x] = find(parent[x]); // Path compression
            }
            return parent[x];
        }
        
        public boolean union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            
            if (rootX == rootY) return false;
            
            // Union by rank
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
            
            return true;
        }
    }
    
    // Number of Provinces using Union-Find
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        UnionFind uf = new UnionFind(n);
        
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (isConnected[i][j] == 1) {
                    uf.union(i, j);
                }
            }
        }
        
        Set<Integer> provinces = new HashSet<>();
        for (int i = 0; i < n; i++) {
            provinces.add(uf.find(i));
        }
        
        return provinces.size();
    }
    
    // Critical Connections (Bridges) - Tarjan's Algorithm Preview
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        // Build graph
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<>());
        }
        
        for (List<Integer> edge : connections) {
            graph.get(edge.get(0)).add(edge.get(1));
            graph.get(edge.get(1)).add(edge.get(0));
        }
        
        // Tarjan's algorithm
        List<List<Integer>> bridges = new ArrayList<>();
        int[] ids = new int[n];
        int[] low = new int[n];
        boolean[] visited = new boolean[n];
        Arrays.fill(ids, -1);
        
        for (int i = 0; i < n; i++) {
            if (ids[i] == -1) {
                dfs(i, -1, ids, low, visited, graph, bridges, new int[]{0});
            }
        }
        
        return bridges;
    }
    
    private void dfs(int node, int parent, int[] ids, int[] low, 
                    boolean[] visited, Map<Integer, List<Integer>> graph,
                    List<List<Integer>> bridges, int[] time) {
        visited[node] = true;
        ids[node] = low[node] = time[0]++;
        
        for (int neighbor : graph.get(node)) {
            if (neighbor == parent) continue;
            
            if (visited[neighbor]) {
                low[node] = Math.min(low[node], ids[neighbor]);
            } else {
                dfs(neighbor, node, ids, low, visited, graph, bridges, time);
                low[node] = Math.min(low[node], low[neighbor]);
                
                if (ids[node] < low[neighbor]) {
                    bridges.add(Arrays.asList(node, neighbor));
                }
            }
        }
    }
}
```

### 🌙 **Evening Session (30 minutes)**
#### Week 6 Complete Reference
```java
// WEEK 6 GRAPH MASTERY REFERENCE

/* ========== REPRESENTATIONS ========== */
// 1. Adjacency List: Map<Integer, List<Integer>>
//    - Space: O(V + E)
//    - Good for sparse graphs
//
// 2. Adjacency Matrix: int[][]
//    - Space: O(V²)
//    - Good for dense graphs
//
// 3. Edge List: List<int[]>
//    - Space: O(E)
//    - Good for algorithms like Kruskal's

/* ========== TRAVERSAL PATTERNS ========== */
// DFS:
// - Recursion or Stack
// - Path finding, cycle detection
// - Connected components
// - Topological sort
// - Time: O(V + E)

// BFS:
// - Queue
// - Shortest path (unweighted)
// - Level-order traversal
// - Multi-source BFS
// - Time: O(V + E)

/* ========== KEY ALGORITHMS ========== */
// 1. Cycle Detection:
//    - Undirected: DFS with parent
//    - Directed: Three colors or Kahn's
//
// 2. Topological Sort:
//    - DFS (reverse postorder)
//    - BFS (Kahn's algorithm)
//
// 3. Bipartite Check:
//    - Two-coloring with BFS/DFS
//
// 4. Connected Components:
//    - DFS/BFS from unvisited nodes

/* ========== GRID AS GRAPH ========== */
// - Each cell is a node
// - 4/8 directional edges
// - DFS/BFS with bounds checking
// - Common: islands, paths, regions

/* ========== COMMON PATTERNS ========== */
// 1. Build graph from input
// 2. Choose traversal method
// 3. Track visited nodes
// 4. Process based on problem
// 5. Return result

/* ========== COMPLEXITY ANALYSIS ========== */
// V = vertices, E = edges
// DFS/BFS: O(V + E) time, O(V) space
// Building graph: O(E) time
// Cycle detection: O(V + E)
// Topological sort: O(V + E)

/* ========== INTERVIEW TIPS ========== */
// 1. Clarify directed vs undirected
// 2. Check for self-loops, multi-edges
// 3. Consider disconnected components
// 4. Draw small examples
// 5. Think about edge cases (empty, single node)
```

### 📝 **Day 7 Final Checklist**
- [ ] Complete assessment quiz
- [ ] Review all graph patterns
- [ ] Finish at least 15 graph problems
- [ ] Create personal notes
- [ ] Ready for Week 7: Dynamic Programming

---

## 🎯 **End of Week 6 Milestones**

### You Should Now Be Able To:
✅ Build graph representations from various inputs  
✅ Implement DFS and BFS confidently  
✅ Detect cycles in directed/undirected graphs  
✅ Perform topological sorting  
✅ Check if graph is bipartite  
✅ Solve island/grid problems efficiently  

### Problems Completed (Minimum):
- ✅ Number of Islands
- ✅ Flood Fill
- ✅ Clone Graph
- ✅ Course Schedule I & II
- ✅ Rotting Oranges
- ✅ Is Graph Bipartite
- ✅ Pacific Atlantic Water Flow

### Core Patterns Mastered:
1. **DFS Applications** - Paths, cycles, components
2. **BFS Applications** - Shortest path, multi-source
3. **Grid Traversal** - Islands, regions, paths
4. **Cycle Detection** - Different techniques
5. **Graph Coloring** - Bipartite, prerequisites

### Skills Developed:
- 🎯 Graph construction from problems
- 🎯 Choosing appropriate traversal
- 🎯 Handling visited state
- 🎯 Multi-source BFS technique
- 🎯 Topological ordering

### Prepare for Week 7:
- Dynamic Programming is very different
- Focus on breaking problems into subproblems
- Memoization and optimal substructure
- Review recursion if needed

## 💪 **Week 6 Reflection Questions**
1. How do graphs compare to trees in complexity?
2. When would you choose DFS over BFS?
3. What was the most challenging graph concept?
4. Can you explain cycle detection to someone?
5. How confident are you with grid problems?

## 🎉 **Excellent Achievement!**
Graphs are one of the most versatile data structures, appearing in countless real-world applications from social networks to GPS navigation. Your mastery of graph traversals, cycle detection, and topological sorting has equipped you with powerful problem-solving tools. The ability to model problems as graphs and apply appropriate algorithms is a mark of advanced programming skill. Next week's Dynamic Programming will challenge you differently - instead of traversal, you'll focus on optimization and breaking down complex problems. Keep building on this strong foundation!
