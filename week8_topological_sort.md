# Fall 2023

# CS 35L

# Discussion 1D

# Week 7



## Anouncement

* Workshop for Project
  * Today 7pm, zoom

## Resources:

Reference: [Pro Git 2nd Edition](https://git-scm.com/book/en/v2) 

Assignment6: Chapter 10.1 - 10.4

<img src="https://git-scm.com/images/progit2.png" style="zoom:50%;" />

[Tutorial made by Sashwath on YouTube](https://www.youtube.com/watch?v=r1wGH5b3V2E)





## Directed Acyclic Graph (DAG)

```mermaid
flowchart TB
    A6 --> A5 --> A4 --> A3 --> A2 --> A1
    AB --> B2 --> B1  --> A2
    AB --> A4
    C2 --> C1 --> B2
    ABC --> AB
    ABC --> C2
    class A1,A2,A3,A4,A5,A6 main
    class B1,B2 branch
    class C1,C2 branch2
    classDef main fill:#f96;
    classDef branch fill:#bbf;
    classDef branch2 fill:#bff;
```

* Directed
* Acyclic (No Cycle)

##### Git Graph

```mermaid
flowchart RL
    A6 --> A5 --> A4 --> A3 --> A2 --> A1
    AB --> B2 --> B1  --> A2
    AB --> A4
    C2 --> C1 --> B2
    ABC --> AB
    ABC --> C2
    class A1,A2,A3,A4,A5,A6 main
    class B1,B2 branch
    class C1,C2 branch2
    classDef main fill:#f96;
    classDef branch fill:#bbf;
    classDef branch2 fill:#bff;
```



## Topological Sort

* Topological Sort  <---->  DAG

```
L ← Empty list that will contain the sorted elements
S ← Set of all nodes with no incoming edge

while S is not empty do
    remove a node n from S
    add n to L
    for each node m with an edge e from n to m do
        remove edge e from the graph
        if m has no other incoming edges then
            insert m into S

if graph has edges then
    return error   (graph has at least one cycle)
else 
    return L   (a topologically sorted order)
```

* for every directed edge *uv* from vertex *u* to vertex *v*, *u* comes **before** *v* in the ordering

## Example

```mermaid
graph TD
		MATH61["MATH 61"]
    CS111["CS 111"]
    CS118["CS 118"]
    CS130["CS 130"]
    CS131["CS 131"]
    CS132["CS 132"]
    CS133["CS 133"]
    CS136["CS 136"]
    CS143["CS 143"]
    CS145["CS 145"]
    CS146["CSM 146"]
    CS152A["CS M152A"]
    CS151B["CS M151B"]
    CS152B["CS 152B"]
    CS161["CS 161"]
    MATH170A["MATH 170A"]
    CS174A["CS 174A"]
    CS174B["CS 174B"]
    CS180["CS 180"]
    CS181["CS 181"]
    CS183["CS 183"]
    CS31["CS 31"]
    CS32["CS 32"]
    CS33["CS 33"]
    CS35L["CS 35L"]
    CS51A["CS M51A"]
    UCLA["Admitted to UCLA"]

		UCLA --> CS31
		UCLA --> CS51A
		UCLA --> MATH170A
		UCLA --> MATH61
		
    CS31 --> CS32
    CS32 --> CS33
    CS32 --> CS143
    CS143 --> CS145
    CS32 --> CS174A
    CS174A --> CS174B
    MATH61 --> CS180
    CS32 --> CS180
    CS180 --> CS181
    CS180 --> CS183
    CS180 --> CS161
    CS33 --> CS151B
    CS151B --> CS152B
    MATH170A --> CS146
    CS33 --> CS146
    CS31 --> CS35L
    CS35L --> CS111
    CS111 --> CS118
    CS118 --> CS136
    CS111 --> CS130
    CS35L --> CS131
    CS131 --> CS130
    CS131 --> CS152B
    CS131 --> CS132
    CS131 --> CS133
    CS151B --> CS133
    CS51A --> CS152A
    CS51A --> CS151B

		class CS143,CS111,CS131,CS33,CS174A,CS180 branch
    class CS35L,CS32,CS152A main
    class MATH61,MATH170A,CS51A,CS31 branch2
    classDef main fill:#f96;
    classDef branch fill:#bbf;
    classDef branch2 fill:#bff;
    
```

```
L = {}
S = {'Admitted to UCLA'}
```

### Next

```mermaid
graph TD
		MATH61["MATH 61"]
    CS111["CS 111"]
    CS118["CS 118"]
    CS130["CS 130"]
    CS131["CS 131"]
    CS132["CS 132"]
    CS133["CS 133"]
    CS136["CS 136"]
    CS143["CS 143"]
    CS145["CS 145"]
    CS146["CSM 146"]
    CS152A["CS M152A"]
    CS151B["CS M151B"]
    CS152B["CS 152B"]
    CS161["CS 161"]
    MATH170A["MATH 170A"]
    CS174A["CS 174A"]
    CS174B["CS 174B"]
    CS180["CS 180"]
    CS181["CS 181"]
    CS183["CS 183"]
    CS31["CS 31"]
    CS32["CS 32"]
    CS33["CS 33"]
    CS35L["CS 35L"]
    CS51A["CS M51A"]
		
    CS31 --> CS32
    CS32 --> CS33
    CS32 --> CS143
    CS143 --> CS145
    CS32 --> CS174A
    CS174A --> CS174B
    MATH61 --> CS180
    CS32 --> CS180
    CS180 --> CS181
    CS180 --> CS183
    CS180 --> CS161
    CS33 --> CS151B
    CS151B --> CS152B
    MATH170A --> CS146
    CS33 --> CS146
    CS31 --> CS35L
    CS35L --> CS111
    CS111 --> CS118
    CS118 --> CS136
    CS111 --> CS130
    CS35L --> CS131
    CS131 --> CS130
    CS131 --> CS152B
    CS131 --> CS132
    CS131 --> CS133
    CS151B --> CS133
    CS51A --> CS152A
    CS51A --> CS151B

		class CS143,CS111,CS131,CS33,CS174A,CS180 branch
    class CS35L,CS32,CS152A main
    class MATH61,MATH170A,CS51A,CS31 branch2
    classDef main fill:#f96;
    classDef branch fill:#bbf;
    classDef branch2 fill:#bff;
```

```
L = {'Admitted to UCLA'}
S = {'CS31', 'MATH 170A', 'CS M51A', 'MATH 61'}
```

### Next

For example, I take CS 31, MATH 61, and CS M51A in one quarter

```mermaid
graph TD
    CS111["CS 111"]
    CS118["CS 118"]
    CS130["CS 130"]
    CS131["CS 131"]
    CS132["CS 132"]
    CS133["CS 133"]
    CS136["CS 136"]
    CS143["CS 143"]
    CS145["CS 145"]
    CS146["CSM 146"]
    CS152A["CS M152A"]
    CS151B["CS M151B"]
    CS152B["CS 152B"]
    CS161["CS 161"]
    MATH170A["MATH 170A"]
    CS174A["CS 174A"]
    CS174B["CS 174B"]
    CS180["CS 180"]
    CS181["CS 181"]
    CS183["CS 183"]
    CS32["CS 32"]
    CS33["CS 33"]
    CS35L["CS 35L"]
		
    CS32 --> CS33
    CS32 --> CS143
    CS143 --> CS145
    CS32 --> CS174A
    CS174A --> CS174B
    CS32 --> CS180
    CS180 --> CS181
    CS180 --> CS183
    CS180 --> CS161
    CS33 --> CS151B
    CS151B --> CS152B
    MATH170A --> CS146
    CS33 --> CS146
    CS35L --> CS111
    CS111 --> CS118
    CS118 --> CS136
    CS111 --> CS130
    CS35L --> CS131
    CS131 --> CS130
    CS131 --> CS152B
    CS131 --> CS132
    CS131 --> CS133
    CS151B --> CS133

		class CS143,CS111,CS131,CS33,CS174A,CS180,CS152A main
    class CS151B,CS146,CS145,CS161,CS174B,CS181,CS183,CS118,CS130,CS132 branch
    class MATH170A,CS32,CS152A,CS35L branch2
    classDef main fill:#f96;
    classDef branch fill:#bbf;
    classDef branch2 fill:#bff;
```

```
L = {'Admitted to UCLA', 'CS31', 'CS M51A', 'MATH 61'}
S = {'MATH 170A', 'CS35L', 'CS M152A', 'CS 32'}
```

### Next

For example, I take CS 32, CS 35L, and CS M152A this quarter

```mermaid
graph TD
    CS111["CS 111"]
    CS118["CS 118"]
    CS130["CS 130"]
    CS131["CS 131"]
    CS132["CS 132"]
    CS133["CS 133"]
    CS136["CS 136"]
    CS143["CS 143"]
    CS145["CS 145"]
    CS146["CSM 146"]
    CS151B["CS M151B"]
    CS152B["CS 152B"]
    CS161["CS 161"]
    MATH170A["MATH 170A"]
    CS174A["CS 174A"]
    CS174B["CS 174B"]
    CS180["CS 180"]
    CS181["CS 181"]
    CS183["CS 183"]
    CS33["CS 33"]
		
    CS143 --> CS145
    CS174A --> CS174B
    CS180 --> CS181
    CS180 --> CS183
    CS180 --> CS161
    CS33 --> CS151B
    CS151B --> CS152B
    MATH170A --> CS146
    CS33 --> CS146
    CS111 --> CS118
    CS118 --> CS136
    CS111 --> CS130
    CS131 --> CS130
    CS131 --> CS152B
    CS131 --> CS132
    CS131 --> CS133
    CS151B --> CS133

    class MATH170A,CS32,CS143,CS33,CS174A,CS180,CS111,CS131 branch2
    classDef main fill:#f96;
    classDef branch fill:#bbf;
    classDef branch2 fill:#bff;
```

```
L = {'Admitted to UCLA', 'CS31', 'CS M51A', 'MATH 61','CS35L', 'CS M152A', 'CS 32'}
S = {'MATH 170A', 'CS 111', 'CS 131', 'CS 143', 'CS 33', 'CS 174A', 'CS 180'}
```



## Final Review

###### 1a) If you use Github to store your class project souce code, what is your failure model for backups, and what are the most important failures to worry about?

* `git rm -rf`
* `git merge --abort`
* Attacker

<details>     
  <summary>Possible Answer</summary>     
  <p style="color: red"> delete data, trash data, messed up when using `git rebase`</p>
</details>



###### 1b) What backup strategy should work well for these failures?
