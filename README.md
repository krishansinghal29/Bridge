/*
// Sample code to perform I/O:

#include <iostream>

using namespace std;

int main() {
	int num;
	cin >> num;										// Reading input from STDIN
	cout << "Input number is " << num << endl;		// Writing output to STDOUT
}

// Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
*/

// Write your code here
#include <iostream>
#include <bits/stdc++.h>
using namespace std;
int min(int a,int b){
    if(a>b){
        return b;
    }
    else{
        return a;
    }
}
struct vlist{
    vlist *p=NULL;
    int key=0;
    vlist *curr=NULL;
    int f=0;
    int color=0;
    int d=1000000;
    int low=1000000;
    vlist *parent=NULL;
};
int t;
int tim=0;
void DFS2(vlist* arr,vlist* u,int e1,int e2){
    arr[u->key-1].color=1;
    tim++;
    arr[u->key-1].d=tim;
    //u->d=tim;
    arr[u->key-1].low=arr[u->key-1].d;
    //u->low=u->d;
    vlist* v=u->p;
    while(v!=NULL){
        //vlist* v=u->p;
        if(arr[v->key-1].color==0){
            arr[v->key-1].parent=&arr[u->key-1];
            DFS2(arr,arr+arr[v->key-1].key-1,e1,e2);
            // if(v->key==e2&&u->key==e1&&arr[v->key-1].low==arr[v->key-1].d){
            //     printf("Bridge\n");
            //     t=1;
            //     return ;
            // }
            // else if(v->key==e2&&u->key==e1){
            //     printf("Not Bridge\n");
            //     return;
            // }
            arr[u->key-1].low=min(arr[u->key-1].low,arr[v->key-1].low);
        }
        else if((arr[v->key-1].color==1)&&(&arr[v->key-1])!=arr[u->key-1].parent){
            arr[u->key-1].low=min(arr[u->key-1].low,arr[v->key-1].d);
        }
        v=v->p;
    }
    tim++;
    arr[u->key-1].color=2;
}
void DFS(vlist* arr,vlist* u,int e1,int e2){
    arr[u->key-1].color=1;
    tim++;
    arr[u->key-1].d=tim;
    //u->d=tim;
    arr[u->key-1].low=arr[u->key-1].d;
    //u->low=u->d;
    vlist* v=u->p;
    while(v!=NULL){
        //vlist* v=u->p;
        if(arr[v->key-1].color==0){
            arr[v->key-1].parent=&arr[u->key-1];
            DFS2(arr,arr+arr[v->key-1].key-1,e1,e2);
            if(v->key==e2&&u->key==e1&&arr[v->key-1].low==arr[v->key-1].d){
                printf("Bridge\n");
                t=1;
                return ;
            }
            // else if(v->key==e2&&u->key==e1){
            //     printf("Not Bridge\n");
            //     return;
            // }
            arr[u->key-1].low=min(arr[u->key-1].low,arr[v->key-1].low);
        }
        else if((arr[v->key-1].color==1)&&(&arr[v->key-1])!=arr[u->key-1].parent){
            arr[u->key-1].low=min(arr[u->key-1].low,arr[v->key-1].d);
        }
        v=v->p;
    }
    tim++;
    arr[u->key-1].color=2;
}
int main(){
	int numtest;
	scanf("%d\n",&numtest);								
	for(int i=0 ;i<numtest;i++){
	    int v;
	    scanf("%d\n",&v);
	    int e;
	    scanf("%d\n",&e);
	    vlist* arr=(vlist *) malloc(v*sizeof(vlist));
	    for(int j=0 ;j<v;j++){
	        arr[j].key=j+1;
	    }
	    //vlist arr[v];
	    for(int j=0 ;j<e;j++){
	        int e1,e2;
	        scanf("%d %d\n",&e1,&e2);
	        if(arr[e1-1].f==0){
	            arr[e1-1].p=(vlist *) malloc(sizeof(vlist));
	            arr[e1-1].p->key=e2;
	            arr[e1-1].f=1;
	            arr[e1-1].curr=arr[e1-1].p;
	        }
	        else{
	            arr[e1-1].curr->p=(vlist *) malloc(sizeof(vlist));
	            arr[e1-1].curr->p->key=e2;
	            arr[e1-1].curr=arr[e1-1].curr->p;
	        }
	        if(arr[e2-1].f==0){
	            arr[e2-1].p=(vlist *) malloc(sizeof(vlist));
	            arr[e2-1].p->key=e1;
	            arr[e2-1].f=1;
	            arr[e2-1].curr=arr[e2-1].p;
	        }
	        else{
	            arr[e2-1].curr->p=(vlist *) malloc(sizeof(vlist));
	            arr[e2-1].curr->p->key=e1;
	            arr[e2-1].curr=arr[e2-1].curr->p;
	        }
	    }
	    tim=0;
	    int e1,e2;
	    scanf("%d %d\n",&e1,&e2);
	    t=0;
	    DFS(arr,arr+e1-1,e1,e2);
	   // for(int i=0;i<v;i++){
	   //     if (arr[i].color==0){
	   //         DFS(arr,arr+i,e1,e2);
	   //     }
	   // }
	    if(t==0){
	        printf("Not Bridge\n");
	    }
	   // else if(t==0&&e<=1){
	   //     printf("Bridge\n");
	   // }
	   // for(int i=0;i<v;i++){
	   //     if (arr[v].color==0){
	   //         DFS(arr[v],e1,e2);
	   //     }
	   // }
	    
	    
	}
	return 0;
}
