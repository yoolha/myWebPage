---
title: "SecondBlog"
date: 2023-05-15T08:14:46Z
draft: true
---

-자료구조 10주차 실습

#include <iostream>
#include <queue>
#include <string>

using namespace std;

class Employee {
public:
    string name;
    string position;

    Employee(const string& name, const string& position)
        : name(name), position(position) {}

    void printInfo() {
        cout << "Name: " << name << ", Position: " << position << endl;
    }
};

class BinaryTree {
private:
    struct Node {
        Employee data;
        Node* left;
        Node* right;
    };

    Node* root;

public:
    BinaryTree() : root(nullptr) {}

    void insert(const Employee& employee) {
        Node* newNode = new Node{ employee, nullptr, nullptr};
        if (root == nullptr) {
            root = newNode;
            return;
        }

        queue<Node*> nodeQueue;
        nodeQueue.push(root);
        while (!nodeQueue.empty()) {
            Node* current = nodeQueue.front();
            nodeQueue.pop();

            if (current->left != nullptr) {
                nodeQueue.push(current->left);
            }
            else {
                current->left = newNode;
                return;
            }

            if (current->right != nullptr) {
                nodeQueue.push(current->right);
            }
            else{
                current->right = newNode;
                return;
            }

        }
        // TODO: 완전 이진 트리 구조의 규칙을 유지하면서 새로운 노드를 추가(큐를 이용)
    }

    void printPreorder() {
        printPreorder(root);
    }

    void printPreorder(Node* node) {
        if (node == nullptr) {
            return;
        }

        node->data.printInfo();
        printPreorder(node->left);
        printPreorder(node->right);
        // TODO: 전위 순회 방법을 이용하여 트리를 순회하며 정보를 출력
    }

    void printInorder() {
        printInorder(root);
    }

    void printInorder(Node* node) {
        if(node == nullptr) {
            return;
        }

        printInorder(node->left);
        node->data.printInfo();
        printInorder(node->right);
        // TODO: 중위 순회 방법을 이용하여 트리를 순회하며 정보를 출력
    }

    void printPostorder() {
        printPostorder(root);
    }

    void printPostorder(Node* node) {
        if (node == nullptr) {
        return;
        }

        printPostorder(node->left);
        printPostorder(node->right);
        node->data.printInfo();
        // TODO: 후위 순회 방법을 이용하여 트리를 순회하며 정보를 출력
    }
};

int main() {
    BinaryTree tree;
    tree.insert(Employee("Alice", "Manager"));
    tree.insert(Employee("Bob", "Developer"));
    tree.insert(Employee("Cindy", "Designer"));
    tree.insert(Employee("David", "Developer"));
    tree.insert(Employee("Eve", "HR"));

    cout << "Preorder traversal:" << endl;
    tree.printPreorder();
    cout << endl;

    cout << "Inorder traversal:" << endl;
    tree.printInorder();
    cout << endl;

    cout << "Postorder traversal:" << endl;
    tree.printPostorder();
    cout << endl;

/* 출력 결과
Preorder traversal:
Name: Alice, Position: Manager
Name: Bob, Position: Developer
Name: David, Position: Developer
Name: Eve, Position: HR
Name: Cindy, Position: Designer

Inorder traversal:
Name: David, Position: Developer
Name: Bob, Position: Developer
Name: Eve, Position: HR
Name: Alice, Position: Manager
Name: Cindy, Position: Designer

Postorder traversal:
Name: David, Position: Developer
Name: Eve, Position: HR
Name: Bob, Position: Developer
Name: Cindy, Position: Designer
Name: Alice, Position: Manager
*/

    return 0;
}