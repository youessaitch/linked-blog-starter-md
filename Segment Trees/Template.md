```cpp
	class segTree
{
    vector<int> seg;

public:
    segTree(int n)
    {
        seg.resize(4 * n);
    }

    void buildSegTree(int idx, int lo, int hi, vector<int> &a)
    {
        if (lo == hi)
        {
            seg[idx] = a[lo];
            return;
        }

        int mid = (lo + hi) >> 1;

        buildSegTree(2 * idx + 1, lo, mid, a);
        buildSegTree(2 * idx + 2, mid + 1, hi, a);

        seg[idx] = min(seg[2 * idx + 1], seg[2 * idx + 2]);
    }

    int query(int idx, int lo, int hi, int L, int R)
    {
        // no overlap
        if (hi < L || R < lo)
            return INT_MAX;

        // complete overlap
        if (lo >= L && hi <= R)
            return seg[idx];

        // partial overlap
        int mid = (lo + hi) >> 1;
        int left = query(2 * idx + 1, lo, mid, L, R);
        int right = query(2 * idx + 2, mid + 1, hi, L, R);

        return min(left, right);
    }

    void pointUpdate(int idx, int lo, int hi, int i, int val)
    {
        if (lo == hi)
        {
            seg[idx] = val;
            return;
        }

        int mid = (lo + hi) >> 1;
        if (i <= mid)
            pointUpdate(2 * idx + 1, lo, mid, i, val);
        else
            pointUpdate(2 * idx + 2, mid + 1, hi, i, val);

        seg[idx] = min(seg[2 * idx + 1], seg[2 * idx + 2]);
    }
};
