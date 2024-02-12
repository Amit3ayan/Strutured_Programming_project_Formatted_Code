#include <stdio.h>

// Define a structure for representing a node in the graph
struct Node {
    int nodeid;      
    int adjcount;       
    int adjs[10];   
    int costs[10];   
};

// Function to add a new node to the graph
int addNode(struct Node *p, int nid, int count) {
    int i = 0, ncount = count;
    for (i = 0; i < count; i++) {
        if (p[i].nodeid == nid) {
            break;
        }
    }
    if (i == count) {
        p[i].nodeid = nid;
        p[i].adjcount = 0;
        ncount++;
    }
    return ncount;  
}

// Function to add an edge between two nodes in the graph
void addAdjacent(struct Node *p, int nid1, int nid2, int cost, int count) {
    int i = 0, index;
    for (i = 0; i < count; i++) {
        if (p[i].nodeid == nid1) {
            index = i;
            break;
        }
    }
    // Add nid2 as an adjacent node to nid1
    p[index].adjs[p[index].adjcount] = nid2;
    p[index].costs[p[index].adjcount] = cost;
    p[index].adjcount++;   
}

// Function to check if a node is already present in a list
int added(int *list, int lcount, int nid) {
    int i = 0;
    for (i = 0; i < lcount; i++) {
        if (list[i] == nid) {
            return 1;   
        }
    }
    return 0;   
}

int ct = 0;

// Function to recursively find paths between two nodes in the graph
void findpath(struct Node *p, int count, int start, int end, int *list, int *clist, int lcount, int x) {
    int index = 0, i = 0, pp;
    // Check if the current node is the destination node
    if (list[lcount - 1] == end) {
        int tcost = 0;
        pp = 0;
        printf("\n");
        // Check if the forbidden node is present in the path
        for (i = 0; i < lcount; i++) {
            if (list[i] == x) {
                pp = 1; 
                break;
            }
            tcost += clist[i];
        }
        // Print the path excluding the forbidden node
        for (i = 0; i < lcount; i++) {
            if (pp == 0) {
                printf(" %d ", list[i]);
            }
        }
        // Print the total cost of the path
        if (tcost != 0 && pp == 0) {
            ct++;  
            printf(" cost = %d", tcost);
        }
        return;
    }

    for (i = 0; i < count; i++) {
        if (p[i].nodeid == start) {
            index = i;
            break;
        }
    }
    // Explore adjacent nodes recursively
    for (i = 0; i < p[index].adjcount; i++) {
        int a = added(list, lcount, p[index].adjs[i]);
        if (a == 0) {
            list[lcount] = p[index].adjs[i];
            clist[lcount] = p[index].costs[i];
            lcount++;
            findpath(p, count, p[index].adjs[i], end, list, clist, lcount, x);
            lcount--;
        }
    }
}

//Declare a global variable
int xx;

int main() {
    struct Node nodes[50];  
    int nodecount = 0;      
    int n1 = 0, n2 = 0, c = 0;  
    // Loop to input node IDs and edge costs until termination signal is given
    while (1) {
        printf("n1, n2, cost ? ");
        scanf("%d %d %d", &n1, &n2, &c);
        if (n1 == -9 && n2 == -9 && c == -9) {
            break;
        }
        // Add nodes and edges to the graph
        nodecount = addNode(&nodes[0], n1, nodecount);
        nodecount = addNode(&nodes[0], n2, nodecount);
        addAdjacent(&nodes[0], n1, n2, c, nodecount);
        addAdjacent(&nodes[0], n2, n1, c, nodecount);
    }
    int start, end;
    printf("start, end ? ");
    scanf("%d %d", &start, &end);
    int list[50], clist[50], lcount = 0;
    list[0] = start;
    clist[0] = 0;
    lcount = 1;
    printf("\nEnter a forbidden node :");
    scanf("%d", &xx);
    // Find and print paths between the start and end nodes while avoiding the forbidden node
    findpath(nodes, nodecount, start, end, list, clist, lcount, xx);
    printf("\n");
    printf("Number of path : %d", ct);  // Print the total number of valid paths found
    return 0;
}
