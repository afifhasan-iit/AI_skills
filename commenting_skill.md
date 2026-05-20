# Commenting Skill

## Purpose
Apply the user's personal C++ commenting style when writing or editing code. Read this file before adding any comments.

---

## Rules

### 1. Function-level comment — one line above the signature
Every non-trivial function gets exactly one line above it. It must:
- Be a sentence fragment (no period at the end)
- State **what the function does** + **what it returns or mutates** (if non-obvious)
- Mention key **assumptions or preconditions** if they exist
- Never restate the function name word-for-word

```cpp
// splits a leaf when full and new key needs to be inserted, returns new leaf node created after split
Node *splitLeaf(Node *leaf, int key)

// inserts key into the B+ tree, handles root creation and root split, returns (possibly new) root
Node *insert(Node *root, int key)

// returns index of first key in node >= given key (position where key would be inserted or is located)
int findKeyIndex(Node *node, int key)
```

---

### 2. Inline trailing comment — same line as code
Used sparingly for non-obvious details, assumptions, or edge-case caveats. Placed after the code with enough spacing to not feel cramped.

```cpp
void insertInLeaf(Node *leaf, int key)      //inserts key into leaf node in sorted order (assumes leaf has space)
child.assign(ORDER + 2, NULL);              //2 extra for temporary storage during splits
return current;                             //if not found returns leaf where it should be, if found also returns the same leaf
```

Do NOT use inline comments to explain obvious code:
```cpp
// WRONG
i++;    //increment i

// RIGHT — no comment needed
i++;
```

---

### 3. Inside function body — section markers only
Only comment inside a function when a distinct logical phase begins. Never narrate line by line.

```cpp
// create temp array with all keys including new key
vector<int> temp(ORDER + 1, 0);
...

// split point
int split = (ORDER + 1) / 2;
...

// link leaves
newLeaf->next = leaf->next;
leaf->next = newLeaf;
```

---

### 4. Section dividers — for grouping related functions
Use uppercase label dividers to separate logical groups of functions:

```cpp
// ========== DISPLAY FUNCTIONS ==========

// ========== DELETION HELPER FUNCTIONS ==========

// ========== MAIN ==========
```

---

## What to NEVER do
- No `/** */` or Doxygen blocks
- No `@param`, `@return`, `@brief` tags
- No multi-line comments above functions
- No commenting every line inside a function
- No repeating what the code already clearly says
- No periods at the end of comments

---

## Style at a glance

| Where | Format | Purpose |
|---|---|---|
| Above function | `// one line fragment` | what + return + assumption |
| Same line as code | `//note` (trailing) | non-obvious detail or caveat |
| Inside function body | `// phase label` | marks a logical section shift |
| Between function groups | `// ===== LABEL =====` | organizes the file |
