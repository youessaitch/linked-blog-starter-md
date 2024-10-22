1. https://codeforces.com/problemset/problem/339/D
- ```cpp
	#include <bits/stdc++.h>
	using namespace std;
	
	class segTree
	{
	    vector<int> seg;
	
	public:
	    segTree(int n)
	    {
	        seg.resize(4 * n);
	    }
	
	    void buildSegTree(int idx, int lo, int hi, vector<int> &a, int orr)
	    {
	        if (lo == hi)
	        {
	            seg[idx] = a[lo];
	            return;
	        }
	
	        int mid = (lo + hi) >> 1;
	
	        buildSegTree(2 * idx + 1, lo, mid, a, !orr);
	        buildSegTree(2 * idx + 2, mid + 1, hi, a, !orr);
	
	        if (orr)
	            seg[idx] = seg[2 * idx + 1] | seg[2 * idx + 2];
	        else
	            seg[idx] = seg[2 * idx + 1] ^ seg[2 * idx + 2];
	    }
	
	    void pointUpdate(int idx, int lo, int hi, int i, int val, int orr, vector<int> &a)
	    {
	        if (lo == hi)
	        {
	            seg[idx] = val;
	            return;
	        }
	
	        int mid = (lo + hi) >> 1;
	        if (i <= mid)
	            pointUpdate(2 * idx + 1, lo, mid, i, val, !orr, a);
	        else
	            pointUpdate(2 * idx + 2, mid + 1, hi, i, val, !orr, a);
	
	        if (orr)
	            seg[idx] = seg[2 * idx + 1] | seg[2 * idx + 2];
	        else
	            seg[idx] = seg[2 * idx + 1] ^ seg[2 * idx + 2];
	    }
	
	    int getRoot()
	    {
	        return seg[0];
	    }
	};
	
	int main()
	{
	    int n, m;
	    cin >> n >> m;
	    int t = pow(2, n);
	
	    vector<int> v(t);
	
	    for (int i = 0; i < t; i++)
	        cin >> v[i];
	
	    segTree seg(t);
	    int orr = 1; // 0 for xor
	    if (n % 2 == 0)
	        seg.buildSegTree(0, 0, t - 1, v, 0); // xor
	    else
	        seg.buildSegTree(0, 0, t - 1, v, 1); // or
	
	    while (m--)
	    {
	        int p, q;
	        cin >> p >> q;
	
	        if (n % 2 == 0)
	            seg.pointUpdate(0, 0, t - 1, p - 1, q, 0, v); // xor
	        else
	            seg.pointUpdate(0, 0, t - 1, p - 1, q, 1, v); // or
	
	        cout << seg.getRoot() << endl;
	    }
	    return 0;
	}

2. https://codeforces.com/problemset/problem/380/C
- Here we are taking multiple values in one node : {cnt of open, cnt of closed, cnt of full}
- 1 open then 1 close forms a valid pair : '( )';
- ```cpp
	#include <bits/stdc++.h>
	using namespace std;
	
	// lets take the value {open bracket, close bracket, full bracket} in node (cnts of open , close, ..)
	struct info
	{
	    int open, close, full;
	
	    info() : open(0), close(0), full(0) {}
	
	    info(int o, int c, int f)
	    {
	        open = o;
	        close = c;
	        full = f;
	    }
	};
	
	class segTree
	{
	    vector<info> seg;
	
	public:
	    segTree(int n)
	    {
	        seg.resize(4 * n);
	    }
	
	    void buildSegTree(int idx, int lo, int hi, string &a)
	    {
	        if (lo == hi)
	        {
	            seg[idx] = info(a[lo] == '(', a[lo] == ')', 0);
	            return;
	        }
	
	        int mid = (lo + hi) >> 1;
	
	        buildSegTree(2 * idx + 1, lo, mid, a);
	        buildSegTree(2 * idx + 2, mid + 1, hi, a);
	
	        int matched = min(seg[2 * idx + 1].open, seg[2 * idx + 2].close);
	
	        // open
	        seg[idx].open = seg[2 * idx + 1].open + seg[2 * idx + 2].open - matched;
	        // close (fix here)
	        seg[idx].close = seg[2 * idx + 1].close + seg[2 * idx + 2].close - matched;
	
	        // full
	        seg[idx].full = seg[2 * idx + 1].full + seg[2 * idx + 2].full + matched;
	    }
	
	    info query(int idx, int lo, int hi, int L, int R)
	    {
	        // no overlap
	        if (hi < L || R < lo)
	            return info(0, 0, 0);
	
	        // complete overlap
	        if (lo >= L && hi <= R)
	            return seg[idx];
	
	        // partial overlap
	        int mid = (lo + hi) >> 1;
	        auto left = query(2 * idx + 1, lo, mid, L, R);
	        auto right = query(2 * idx + 2, mid + 1, hi, L, R);
	
	        info res;
	        int matched = min(left.open, right.close);
	
	        res.full = left.full + right.full + matched;
	        res.open = left.open + right.open - matched;
	        res.close = left.close + right.close - matched;
	
	        return res;
	    }
	};
	
	int main()
	{
	    string s;
	    cin >> s;
	
	    int n = s.size();
	    segTree seg(n);
	
	    seg.buildSegTree(0, 0, n - 1, s);
	
	    int m;
	    cin >> m;
	
	    while (m--)
	    {
	        int L, R;
	        cin >> L >> R;
	
	        // Adjust 1-based indices to 0-based and multiply result by 2 (since each match involves 2 brackets)
	        cout << seg.query(0, 0, n - 1, L - 1, R - 1).full * 2 << endl;
	    }
	    return 0;
	}

