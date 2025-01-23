# day17
import sys
sys.setrecursionlimit(10000)

# DFS 함수 정의
def dfs(x, y, N, map_data, visited):
    # 상하좌우 방향 정의
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    # 집이 있는 곳을 방문 처리하고 집 수 증가
    visited[x][y] = True
    house_count = 1
    
    # 4방향 탐색
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        
        # 범위 체크 및 방문하지 않은 집 탐색
        if 0 <= nx < N and 0 <= ny < N and not visited[nx][ny] and map_data[nx][ny] == 1:
            house_count += dfs(nx, ny, N, map_data, visited)
    
    return house_count

# 메인 함수
def main():
    # 지도 크기 입력
    N = int(input())
    map_data = [list(map(int, input().strip())) for _ in range(N)]
    
    # 방문 여부를 확인할 배열
    visited = [[False] * N for _ in range(N)]
    
    # 단지들의 크기를 담을 리스트
    complex_sizes = []
    
    # 모든 칸을 탐색하면서 단지를 찾기
    for i in range(N):
        for j in range(N):
            if map_data[i][j] == 1 and not visited[i][j]:
                # 새로운 단지가 발견되면 DFS 실행
                complex_size = dfs(i, j, N, map_data, visited)
                complex_sizes.append(complex_size)
    
    # 단지 수 출력
    print(len(complex_sizes))
    # 단지별 집 수를 오름차순으로 출력
    for size in sorted(complex_sizes):
        print(size)

if __name__ == "__main__":
    main()
