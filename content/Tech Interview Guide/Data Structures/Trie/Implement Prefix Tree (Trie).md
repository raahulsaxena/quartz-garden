---
title: Implement Prefix Tree (Trie)
tags:
    - data-structures
    - trie
    - c++
    - algorithms
created: 2023-07-15
updated: 2025-05-01
---


## Approach

- You first need a separate class altogether (with a constructor) for TrieNode;
	- It should have two properties:
		- isEndOfWord : stores the information whether a current node represents an end of word
		- map of char and TrieNode pointers: This will store the children of the current trie node.
- Now, in the Trie Constructor, you can define a root node
- for insert and search, traverse accordingly. Straightforward logic.
- Time Complexity: O(N), Space Complexity: O(N)

```cpp


class TrieNode{

public:
    unordered_map<char, TrieNode*> children;

    bool isEndOfWord;

    TrieNode() {
        isEndOfWord = false;
    }

};


class Trie {

private:
    TrieNode* root;
public:
    Trie() {
        
        root = new TrieNode();
    }
    
    void insert(string word) {

        TrieNode* node = root;

        for(char ch: word){
            if(node->children.find(ch) == node->children.end()){
                node->children[ch] = new TrieNode();
            }

            node = node->children[ch];
        }

        node->isEndOfWord = true;
        
    }
    
    bool search(string word) {

        TrieNode* node = root;

        for(char ch: word){

            if(node->children.find(ch) == node->children.end()){
                return false;
            }
            
            node = node->children[ch];

        }

        return node->isEndOfWord;
        
    }
    
    bool startsWith(string prefix) {

        TrieNode* node = root;

        for(char ch: prefix){

            if(node->children.find(ch) == node->children.end()) return false;

            node = node->children[ch];

        }

        return true;
        
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```