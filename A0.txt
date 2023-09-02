#include <stdio.h>
#include <time.h>
void dfs(int a[10][10], int n, int sr, int vis[10])
{
  int v;
  printf("%d ", sr);
  vis[sr] = 1;
  for (v = 1; v <= n; v++)
    if (a[sr][v] == 1 && vis[v] == 0)
      dfs(a, n, v, vis);
}
int main()
{
  int a[10][10], n, i, j, s;
  int vis[10] = {0};
  double clk;
  clock_t st, ent;
  printf("Enter the no of lands to be surveyed:");
  scanf("%d", &n);
  printf("Enter the adjacency matrix:\n");
  for (i = 1; i <= n; i++)
    for (j = 1; j <= n; j++)
    {
      if (i == j)
        a[i][j] = 0; // Set diagonal elements to zero
      else
      {
        printf("(%d,%d):", i, j);
        scanf("%d", &a[i][j]);
      }
    }
  printf("Enter the starting land number:");
  scanf("%d", &s);
  st = clock();
  printf("Vertices reached from the given vertex are...\n");
  dfs(a, n, s, vis);
  ent = clock();
  clk = (double)(ent - st) / CLOCKS_PER_SEC;
  printf("\nTime: %f seconds\n", clk);
  return 0;
}

//--------------------------------------------------------------------------------------


#include <stdio.h>
int bfs(int a[10][10], int n, int sr)
{
  int vis[10], q[10], f = 0, r = -1, v, u;
  for (v = 1; v <= n; v++)
    vis[v] = 0;
  q[++r] = sr;
  vis[sr] = 1;
  printf("\nTRAVERSED BFS:\n");
  while (f <= r) // explore
  {
    u = q[f++]; // dequeue the element and explore it completely
    for (v = 1; v <= n; v++)
      if (a[u][v] == 1 && vis[v] == 0)
      {
        q[++r] = v; // add to QUEUE
        vis[v] = 1;
        printf("%d %d \n", u, v);
      }
  }
}
int main()
{
  int a[10][10];
  int i, j, n, s;
  printf("Enter the number of cities: ");
  scanf("%d", &n);
  printf("Enter the matrix representation:\n");
  for (i = 1; i <= n; i++)
    for (j = 1; j <= n; j++)
    {
      if (i == j)
        a[i][j] = 0;
      else
      {
        printf("(%d,%d):", i, j);
        scanf("%d", &a[i][j]);
      }
    }
  printf("Enter the source city: ");
  scanf("%d", &s);
  bfs(a, n, s);
}

//-----------------------------------------------------------------------------

int binary(int a[], int st, int en, int sr)
{
  if (st != en)
  {
    int m;
    m = (st + (en - 1)) / 2;
    if (a[m] == sr)
      return m;
    else if (a[m] > sr)
      return (binary(a, st, (m - 1), sr));
    else if (a[m] < sr)
      return (binary(a, (m + 1), en, sr));
  }
  return -1;
}
//-------------------------------------------------------------------------------

#include <stdio.h>
int main()
{
  int a[] = {4, 7, 1, 42, 8, 9, 23};
  int x, i, j, n = 7;
  for (i = 1; i < n; i++)
  {
    j = i - 1;
    x = a[i];
    while (j >= 0 && a[j] > x)
    {
      a[j + 1] = a[j];
      j--;
    }
    a[j + 1] = x;
  }
  for (i = 0; i < n; i++)
    printf("%d ", a[i]);
}

//---------------------------------------------------------------------------

#include <stdio.h>
#include <stdlib.h>
int ar[20];
void merge(int l, int mid, int h)
{
  int i, j, k;
  i = k = l;
  j = mid + 1;
  int b[100];
  while (i <= mid && j <= h)
  {
    if (ar[i] < ar[j])
      b[k++] = ar[i++];
    else
      b[k++] = ar[j++];
  }
  while (i <= mid)
    b[k++] = ar[i++];
  while (j <= h)
    b[k++] = ar[j++];
  for (i = l; i <= h; i++)
    ar[i] = b[i];
}
void mergesort(int l, int h)
{
  int mid;
  if (l < h)
  {
    mid = (l + h) / 2;
    mergesort(l, mid);
    mergesort(mid + 1, h);
    merge(l, mid, h);
  }
}

//--------------------------------------------------------------------------

#include <stdio.h>
int partition(int a[7], int l, int h)
{
  int pivot = a[l], t, i = l, j = h;
  do
  {
    do
      i++;
    while (a[i] <= pivot);
    do
      j--;
    while (a[j] > pivot);
    if (i < j)
    {
      t = a[i];
      a[i] = a[j];
      a[j] = t;
    }
  } while (i < j);
  t = a[j];
  a[j] = a[l];
  a[l] = t;
  return j;
}
void quicksort(int a[7], int l, int h)
{
  int j;
  if (l < h)
  {
    j = partition(a, l, h);
    quicksort(a, l, j);
    quicksort(a, j + 1, h);
  }
}

//-------------------------------------------------------------------------------

#include <stdio.h>
int A[20] = {0, 10, 20, 30, 25, 5, 40, 35};
void Insert(int n)
{
  int i = n, t;
  t = A[n];
  while (i > 1 && t > A[i / 2])
  {
    A[i] = A[i / 2];
    i = i / 2;
  }
  A[i] = t;
}
int heap(int n) // delete and return the val
{
  int i, x, j, val, t;
  x = A[n];
  val = A[1];
  A[1] = A[n];
  A[n] = val;
  i = 1;
  j = i * 2;
  while (j < n - 1)
  {
    if (A[j + 1] > A[j])
      j = j + 1;
    if (A[j] > A[i])
    {
      t = A[j]; // swap
      A[j] = A[i];
      A[i] = t;
      i = j;
      j = j * 2;
    }
    else
      break;
  }
  return val;
}
int main()
{
  // 40,25,35,10,5,20,30
  int i;
  for (i = 2; i <= 7; i++)
    Insert(i);

  for (i = 7; i > 1; i--)
    heap(i);
  for (i = 1; i <= 7; i++)
    printf("%d ", A[i]);
  printf("\n");
  return 0;
}

//----------------------------------------------------------------

#include <stdio.h>
#include <string.h>
#include <conio.h>
#define MAX 500
int t[MAX];
void shifttable(char p[])
{
  int i, j, m;
  m = strlen(p);
  for (i = 0; i < MAX; i++)
    t[i] = m;
  for (j = 0; j < m - 1; j++)
    t[p[j]] = m - 1 - j;
}
int horspool(char src[], char p[])
{
  int i, j, k, m, n;
  n = strlen(src);
  m = strlen(p);
  printf("Length of text:%d\n", n);
  printf("Length of pattern:%d\n", m);
  i = m - 1;
  while (i < n)
  {
    k = 0;
    while ((k < m) && (p[m - 1 - k] == src[i - k]))
      k++;
    if (k == m)
      return (i - m + 1);
    else
      i += t[src[i]];
  }
  return -1;
}
void main()
{
  char src[100], p[100];
  int pos;

  printf("Enter the text:");
  gets(src);
  printf("Enter the pattern to be searched:");
  gets(p);
  shifttable(p);
  pos = horspool(src, p);
  if (pos >= 0)
    printf("Pattern found starting from position %d\n", pos + 1);
  else
    printf("Pattern not found in the text\n");
}
// ------------------------------------------------------------------------------------

#include <stdio.h>
int min(int a, int b)
{
  if (a < b)
    return a;
  else
    return b;
}

void floyd(int n, int W[10][10], int D[10][10])
{
  int i, j, k;
  for (i = 0; i < n; i++)
    for (j = 0; j < n; j++)
      D[i][j] = W[i][j];
  for (k = 0; k < n; k++)
    for (i = 0; i < n; i++)
      for (j = 0; j < n; j++)
        D[i][j] = min(D[i][j], D[i][k] + D[k][j]);
}

void main()
{
  int i, j, n, D[10][10], W[10][10];
  printf("Enter no.of vertices:");
  scanf("%d", &n);
  printf("Enter the cost matrix:\n");
  for (i = 0; i < n; i++)
    for (j = 0; j < n; j++)
      scanf("%d", &W[i][j]);
  floyd(n, W, D);
  printf("All pair shortest path matrix is:\n");
  for (i = 0; i < n; i++)
  {
    for (j = 0; j < n; j++)
      printf("%d ", D[i][j]);
    printf("\n");
  }
}

// --------------------------------------------------------------------------------------------------------

#include <stdio.h>
int max(int x, int y)
{
  return ((x > y) ? x : y);
}

int knap(int n, int w[10], int val[10], int m, int v[10][10])
{
  int i, j;
  for (i = 0; i <= n; i++)
    for (j = 0; j <= m; j++)
    {
      if (i == 0 || j == 0)
        v[i][j] = 0;
      else if (j < w[i])
        v[i][j] = v[i - 1][j];
      else
        v[i][j] = max(v[i - 1][j], val[i] + v[i - 1][j - w[i]]);
    }
  printf("\n The table for solving knapsack problem using dynamic programming is:\n");
  for (i = 0; i <= n; i++)
  {
    for (j = 0; j <= m; j++)
      printf("%d\t", v[i][j]);
    printf("\n");
  }
}

void main()
{
  int v[10][10], n, i, j, w[10], val[10], m, res;
  printf("Enter the number of items:");
  scanf("%d", &n);
  printf("Enter the weights of %d items:", n);
  for (i = 1; i <= n; i++)
    scanf("%d", &w[i]);
  printf("Enter the value of %d items:", n);
  for (i = 1; i <= n; i++)
    scanf("%d", &val[i]);
  printf("Enter the capacity of the basket:");
  scanf("%d", &m);
  for (i = 0; i <= n; i++)
    for (j = 0; j <= m; j++)
      v[i][j] = 0;
  res = knap(n, w, val, m, v);
  printf("Optimal solution for the knapsack problem is %d\n", v[n][m]);
}

// ----------------------------------------------------------------------------------------------------------------------------------

#include <stdio.h>
#include <time.h>
struct edge
{
  int u, v, cost;
};
typedef struct edge edge;
int find(int v, int parent[])
{
  while (parent[v] != v)
    v = parent[v];
  return v;
}
void union_ij(int i, int j, int parent[])
{
  if (i < j)
    parent[j] = i;
  else
    parent[i] = j;
}
void kruskal(int n, edge e[], int m)
{
  int count, k, i, sum, u, v, j, t[10][10], p, parent[10];
  edge temp;
  count = k = sum = 0;
  for (i = 0; i < m; i++)
    for (j = 0; j < m - 1; j++)
      if (e[j].cost > e[j + 1].cost)
      {
        temp.u = e[j].u;
        temp.v = e[j].v;
        temp.cost = e[j].cost;
        e[j].u = e[j + 1].u;
        e[j].v = e[j + 1].v;
        e[j].cost = e[j + 1].cost;
        e[j + 1].u = temp.u;
        e[j + 1].cost = temp.cost;
      }
  for (i = 0; i < n; i++)
    parent[i] = i;
  p = 0;
  while (count != n - 1)
  {
    u = e[p].u;
    v = e[p].v;
    i = find(u, parent);
    j = find(v, parent);
    if (i != j)
    {
      t[k][0] = u;
      t[k][1] = v;
      k++;
      count++;
      sum += e[p].cost;
      union_ij(i, j, parent);
    }
    p++;
  }
  if (count == n - 1)
  {
    printf("Spanning tree exists\n");
    printf("The spanning tree is as follows:\n");
    for (i = 0; i < n - 1; i++)
    {
      printf("%d  %d\t", t[i][0], t[i][1]);
    }
    printf("\nThe cost of the spanning tree is %d\n", sum);
  }
  else
    printf("\n spanning tree does not exist");
}
void main()
{
  int n, m, a, b, i, cost;
  edge e[20];
  printf("Enter the number of vertices:");
  scanf("%d", &n);
  printf("Enter the number of edges:\n");
  scanf("%d", &m);
  printf("Enter the edge list( u  v  cost)\n");
  for (i = 0; i < m; i++)
  {
    scanf("%d%d%d", &a, &b, &cost);
    e[i].u = a;
    e[i].v = b;
    e[i].cost = cost;
  }
  kruskal(n, e, m);
}
// Enter the number of vertices:6
// Enter the number of edges:
// 10
// Enter the edge list( u  v  cost)
// 0 1 2
// 1 2 4
// 2 3 6
// 3 4 5
// 4 0 8
// 0 5 5
// 1 5 4
// 2 5 4
// 3 5 4
// 4 5 5
// Spanning tree exists
// The spanning tree is as follows:
// 0  1    1  2    1  5    3  5    4  5
// The cost of the spanning tree is 19
// =---------------------------------------------------------------------------------------------

#include <stdio.h>
#include <time.h>
#define MAX 10
int choose(int dist[], int s[], int n)
{
  int j = 1, min = 1000, w;
  for (w = 1; w <= n; w++)
    if ((dist[w] < min) && (s[w] == 0))
    {
      min = dist[w];
      j = w;
    }
  return j;
}

void spath(int v, int cost[][MAX], int dist[], int n)
{
  int w, u, i, num, s[MAX];
  for (i = 1; i <= n; i++)
  {
    s[i] = 0;
    dist[i] = cost[v][i];
  }
  s[v] = 0;
  dist[i] = 999;
  for (num = 2; num <= n; num++)
  {
    u = choose(dist, s, n);
    s[u] = 1;
    for (w = 1; w <= n; w++)
    {

      if ((dist[u] + cost[u][w]) < dist[w] && !s[w])
        dist[w] = dist[u] + cost[u][w];
    }
  }
}

void main()
{
  int i, j, cost[MAX][MAX], dist[MAX], n, v;

  printf("\nEnter number of vertices:");
  scanf("%d", &n);
  printf("\nEnter the cost of adjacency matrix\n");
  for (i = 1; i <= n; i++)
    for (j = 1; j <= n; j++)
      scanf("%d", &cost[i][j]);
  printf("\nEnter the source vertex:");
  scanf("%d", &v);

  spath(v, cost, dist, n);

  printf("\nShortest  distance\n");
  for (i = 1; i <= n; i++)
    printf("\n%d to %d = %d", v, i, dist[i]);
}

// --------------------------------------------------------------------------------------------

#include <stdio.h>
#include <math.h>
#define FALSE 0
#define TRUE 1

int x[20];
int place(int k, int i)
{
  int j;
  for (j = 1; j <= k; j++)
    if ((x[j] == i) || (abs(x[j] - i) == abs(j - k)))
      return FALSE;
  return TRUE;
}
void nqueens(int k, int n)
{
  int i, a;
  for (i = 1; i <= n; i++)
    if (place(k, i))
    {
      x[k] = i;
      if (k == n)
      {
        for (a = 1; a <= n; a++)
          printf("%d\t", x[a]);
        printf("\n");
      }
      else
        nqueens(k + 1, n);
    }
}
void main()
{
  int n;
  printf("\nEnter the number of queens:");
  scanf("%d", &n);
  printf("\n The solution to N Queens problem is: \n");
  nqueens(1, n);
}
// =------------------------------------------------------------------------------------------------------------------------------------------

#include <stdio.h>

int count, w[10], d, x[10];

void subset(int cs, int k, int r)
{
  int i;
  x[k] = 1;
  if (cs + w[k] == d)
  {
    printf("\nSubset solution = %d\n", ++count);
    for (i = 0; i <= k; i++)
    {
      if (x[i] == 1)
        printf("%d ", w[i]);
    }
    printf("\n");
  }
  else if (cs + w[k] + w[k + 1] <= d)
  {
    subset(cs + w[k], k + 1, r - w[k]);
  }
  if (cs + r - w[k] >= d && cs + w[k + 1] <= d)
  {
    x[k] = 0;
    subset(cs, k + 1, r - w[k]);
  }
}

int main()
{
  int sum = 0, i, n;
  printf("Enter the number of elements: ");
  scanf("%d", &n);
  printf("Enter the elements in ascending order: ");
  for (i = 0; i < n; i++)
    scanf("%d", &w[i]);
  printf("Enter the required sum: ");
  scanf("%d", &d);
  for (i = 0; i < n; i++)
    sum += w[i];
  if (sum < d)
  {
    printf("No solution exists.\n");
  }
  else
  {
    printf("The solution is:\n");
    count = 0;
    subset(0, 0, sum);
    if (count == 0)
    {
      printf("No solution exists.\n");
    }
  }
  return 0;
}