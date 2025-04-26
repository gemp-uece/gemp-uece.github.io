---
title: Upsolving MFP primeira fase
date: 2025-04-25 00:38:00 -300
description: Upsolvingo da primeira fase da MFP
author: buzz
categories: [Upsolving, MFP]
tags: [mfp, competicoes, upsolving]
pin: true
math: true
mermaid: true 
---

### A: I'm Still Celebrating!

Link do problema: [A](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/A)

```cpp
#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

bool check(int x,int y, vector<vector<int>> &grid){
    if(x > 10 || x < 0 || y > 10 || y < 0) return false;
    if(grid[x][y] == 1) return false;

    grid[x][y] = 1;
    return true;
}

signed main() { _
    int n, m; cin >> n >> m;
    vector<int> v(n);
    for(int i = 0; i < n; i++){
        cin >> v[i];
    }

    sort(v.begin(),v.end());

    for(int i = 1; i<= m; i++){
        auto pos = lower_bound(v.begin(), v.end(), i);
        cout << distance(pos, v.end()) << " ";
    }
    cout << endl;
    return 0;
}

```

### B: Map of the city

Link do problema: [B](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/B)

```cpp
#include <bits/stdc++.h>
 
using namespace std;
 
#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;
 
const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e5+5;
 
vector<vector<int>> graph(MAX, vector<int>());
vector<int> vis(MAX,0);
 
set<pair<int,int>> edges;
int visited = 0;
 
 
void dfs(int node){
    for(auto e : graph[node]){
        edges.insert({min(e,node), max(e,node)});
        if(vis[e] != 0) continue;
        vis[e] = node;
        dfs(e);
        visited++;
    }
}
 
signed main() { _
    int n, m; cin >> n >> m;
    for(int i = 0; i < m; i++){
        int u,v; cin >> u >> v;
        graph[u].push_back(v);
        graph[v].push_back(u);
    }
    pair<int,int> ans = {0,0};
    for(int i = 1; i <= n; i++){
        if(vis[i] != 0) continue;
        edges.clear();
        visited = 1;
        vis[i] = i;
        dfs(i);
        ans.first++;
        ans.second += abs(visited - 1 - (int)edges.size());
    }
    // cidades visitadas, ciclos encontrados.
    if(ans.first == 1 and ans.second == 0){
        cout << "BOM" << endl;
    } else {
        cout << "RUIM" << " " << ans.second << " " << ans.first - 1 << endl;
    }
    return 0;
}
```

### C: The discrepant sensor

Link do problema: [C](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/C)

```cpp
#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

bool check(int x,int y, vector<vector<int>> &grid){
    if(x > 10 || x < 0 || y > 10 || y < 0) return false;
    if(grid[x][y] == 1) return false;

    grid[x][y] = 1;
    return true;
}

signed main() { _
    int t; cin >> t;
    while(t--){
        int a,b,c; cin >> a >> b >> c;
        if(a == b) cout << c << endl;
        if(b == c) cout << a << endl;
        if(a == c) cout << b << endl;
    }
    return 0;
}

```

### D: UNICAMP Circles (Unsolved yet)

Link do problema: [D](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/D)

```cpp
```

### E: Reverse Engineering

Link do problema: [E](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/E)

```cpp
#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e5+5;
const static double PI = acos(-1);

signed main() { _
    int n, m; cin >> n >> m;
    vector<vector<int>> apples(n,vector<int>(m));
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            cin >> apples[i][j];
        }
    }
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            apples[i][j] = apples[i][j] + ((apples[i][j] + i + j) % 2);
        }
    }
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            cout << apples[i][j] << " ";
        }
        cout << endl;
    }
    return 0;
}

```

### F: Duck-duck-goose

Link do problema: [F](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/F)

```cpp
#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e5+5;


signed main() { _
    int n,p,k; cin >> n >> p >> k;
    vector<int> v;
    for(int i = p+1; i <= n; i++){
        v.push_back(i);
    }
    for(int i = 1; i< p; i++){
        v.push_back(i);
    }
    int ans = 0;
    n--;
    k++;
    while(k > 0){
        for(int i = 0; i < v.size() && k > 0; i++, k--){
            ans = v[i];
        }
    }
    cout << ans << endl;
    return 0;
}

```

### G: Mixer for Phrases

Link do problema: [G](https://codeforces.com/group/9CNwiex6Ir/contest/606592/problem/G)

```cpp
#include <bits/stdc++.h>

using namespace std;

#define _ ios_base::sync_with_stdio(0);cin.tie(0);
#define endl '\n'
#define int long long
typedef long long ll;

const int INF = 0x3f3f3f3f;
const ll LINF = 0x3f3f3f3f3f3f3f3fll;
const long long MOD = 1e9 + 7;
const int MAX = 1e6+5;

signed main() { _
    string s; cin >> s;
    string a = "";
    string b = "";
    for(int i = 0; i < s.size(); i++){
        if(i % 2 == 0){
            a += s[i];
        } else {
            b += s[i];
        }
    }
    cout << a << endl;
    cout << b << endl;
    return 0;
}

```