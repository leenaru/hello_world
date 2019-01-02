# DFS

##### Tree 탐색

```c
#define LEN_STACK   128
#define LEN 7
#define TRUE    1
#define FALSE   0
#define ERROR   -1


int stack[LEN_STACK];
int idx = 0;

void create_stack()
{
    stack[LEN_STACK] = { 0 };
}

void print_stack()
{
    for (int i = 0; i < idx; i++)
        printf("[%d]\t", stack[i]);

    printf("\n");
}

int push(int p)
{
    stack[idx++] = p;

    if (idx >= LEN_STACK)
        return ERROR;
    else
        return p;
}

int pop()
{
    if (idx == 0)
        return ERROR;
    else
        return stack[--idx];
}

int visited[LEN + 1];

bool isAdjacent(int v, int adj[LEN + 1][LEN + 1], int* w)
{
    for (int i = 1; i < LEN + 1; i++)
    {
        if (((adj[v][i] == TRUE) || (adj[i][v] == TRUE)) && (visited[i] == FALSE))
        {
            *w = i;
            return true;
        }
    }
    return false;
}

int DFS(int arr[LEN + 1][LEN + 1], int size, int result[LEN])
{
    for (int i = 1; i < LEN + 1; i++)
    {
        visited[i] = FALSE;
    }

    create_stack();
    int v = 1;
    int w = v;
    int index = 0;

    push(w);
    print_stack();
    visited[w] = TRUE;
    result[index++] = w;

    do
    {
        if (isAdjacent(v, arr, &w))
        {
            push(v);
            print_stack();
            visited[w] = TRUE;
            result[index++] = w;
            v = w;
        }
        else
        {
            v = pop();
            print_stack();
        }
    } while (idx > 0);

    return 0;
}

int main()
{
    int arr[LEN + 1][LEN + 1] = { 0 };

    // 1,2, 1,3, 2,4, 2,5, 4,6, 5,6, 6,7, 3,7
    // 1-2-4-6-5-7-3

    arr[1][2] = 1;
    arr[1][3] = 1;
    arr[2][4] = 1;
    arr[2][5] = 1;
    arr[4][6] = 1;
    arr[5][6] = 1;
    arr[6][7] = 1;
    arr[3][7] = 1;

    int out[LEN] = { 0 };
    DFS(arr, LEN, out);

    for (int i = 0; i < LEN; i++)
        printf("%d-", out[i]);

    printf("\n");

    return 0;
}
```

##### Grid 탐색
```

```
