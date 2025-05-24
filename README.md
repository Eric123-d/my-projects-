# my-projects-
1. C 语言
2. Python
3. import heapq

def dijkstra(graph, start):
    """
    graph: dict，键是节点，值是列表，表示邻居和边权重，比如：
           { 'A': [('B', 5), ('C', 2)],
             'B': [('A', 5), ('C', 1), ('D', 3)],
             ... }
    start: 起点节点
    返回：从start到每个节点的最短距离
    """

    # 初始化距离，默认无穷大
    distances = {node: float('inf') for node in graph}
    distances[start] = 0  # 起点距离自己为0

    # 优先队列，存储(距离，节点)
    pq = [(0, start)]

    while pq:
        current_distance, current_node = heapq.heappop(pq)

        # 如果已经找到更短距离，跳过
        if current_distance > distances[current_node]:
            continue

        # 遍历邻居
        for neighbor, weight in graph[current_node]:
            distance = current_distance + weight

            # 如果找到更短路径，更新并加入队列
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))

    return distances


# 测试
graph_example = {
    'A': [('B', 5), ('C', 2)],
    'B': [('A', 5), ('C', 1), ('D', 3)],
    'C': [('A', 2), ('B', 1), ('D', 7)],
    'D': [('B', 3), ('C', 7)]
}

result = dijkstra(graph_example, 'A')
print(result)
