#include <iostream>
#include <vector>
using namespace std;
struct Node{
    int data;
    Node *left,*right;
};
Node*newNode(int v){
    Node* temp=new Node();
    temp->data=v;
    temp->right=temp->left=nullptr;
    return temp;
}
Node* insertLevelOrder(vector<int>arr,int start,int size){
    Node* temp=nullptr;
    if(start<size){
        temp=newNode(arr[start]);
        temp->left=insertLevelOrder(arr,2*start+1,size);
        temp->right=insertLevelOrder(arr,2*start+2,size);
    }
    return temp;
}
void printInorder(Node*node){
    if(node==nullptr){
        return;
    }
    printInorder(node->left);
    cout<<node->data<<" ";
    printInorder(node->right);
}
int main(){
    vector<int>arr;
    int num;
    while(cin>>num){
        arr.push_back(num);
    }
    int a=arr.size();
    Node*root=nullptr;
    root=insertLevelOrder(arr,0,a);
    printInorder(root);
}
