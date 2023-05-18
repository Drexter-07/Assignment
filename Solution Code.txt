#include<bits/stdc++.h>
using namespace std;

class Solution {
public:
    int minTime(vector<vector<int>>& times, int n, int k) {
         vector<vector<pair<int, int>>> graph(n + 1);
        vector<int> distToNodes(n + 1, INT_MAX);
        distToNodes[k] = 0;

        for(auto &edge : times)
            graph[edge[0]].push_back({edge[1], edge[2]});

        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        pq.push({0, k});

        while(!pq.empty()) {
            int u = pq.top().second;
            pq.pop();

            for(auto &neighbour : graph[u]) {
                int v = neighbour.first, w = neighbour.second;
                if(distToNodes[u] + w < distToNodes[v]) {
                    distToNodes[v] = distToNodes[u] + w;
                    pq.push({distToNodes[v], v});
                }
            }
        }

        int max_time = *max_element(distToNodes.begin() + 1, distToNodes.end());
        return max_time == INT_MAX ? -1 : max_time;
    }
};

int main() {
    Solution s;
    //vector<vector<int>> input as given in the question
    vector<vector<int>> times = {{2,1,1},{2,3,1},{3,4,1}};
    int n = 4, k = 2;
    cout << "Output: " << s.minTime(times, n, k) << endl;
    //Output: 2, according to the input provided
    return 0;
}