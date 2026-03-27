# discrete-maths
# practical 1
#include <iostream>
using namespace std;

class SET {
public:
    int a[10], n;

    void input() {
        cout << "Enter number of elements: ";
        cin >> n;
        cout << "Enter elements: ";
        for (int i = 0; i < n; i++)
            cin >> a[i];
    }

    void display() {
        cout << "{ ";
        for (int i = 0; i < n; i++)
            cout << a[i] << " ";
        cout << "}\n";
    }

    // isMember
    bool isMember(int x) {
        for (int i = 0; i < n; i++)
            if (a[i] == x) return true;
        return false;
    }

    // Union
    void setUnion(SET b) {
        SET c = *this;
        for (int i = 0; i < b.n; i++) {
            if (!c.isMember(b.a[i])) {
                c.a[c.n++] = b.a[i];
            }
        }
        c.display();
    }

    // Intersection
    void intersection(SET b) {
        SET c;
        c.n = 0;
        for (int i = 0; i < n; i++) {
            if (b.isMember(a[i]))
                c.a[c.n++] = a[i];
        }
        c.display();
    }

    // Difference A-B
    void difference(SET b) {
        SET c;
        c.n = 0;
        for (int i = 0; i < n; i++) {
            if (!b.isMember(a[i]))
                c.a[c.n++] = a[i];
        }
        c.display();
    }
};

int main() {
    SET A, B;
    int ch, x;

    cout << "Enter Set A:\n";
    A.input();

    cout << "Enter Set B:\n";
    B.input();

    do {
        cout << "\n1.Member 2.Union 3.Intersection 4.Difference 0.Exit\n";
        cin >> ch;

        switch (ch) {
        case 1:
            cout << "Enter element: ";
            cin >> x;
            if (A.isMember(x)) cout << "Present\n";
            else cout << "Not Present\n";
            break;

        case 2:
            A.setUnion(B);
            break;

        case 3:
            A.intersection(B);
            break;

        case 4:
            A.difference(B);
            break;
        }
    } while (ch != 0);

    return 0;
}

# practical 2
#include <iostream>
using namespace std;

class RELATION {
public:
    int n, r[10][10];

    void input() {
        cout << "Enter number of elements: ";
        cin >> n;
        cout << "Enter relation matrix:\n";
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cin >> r[i][j];
    }

    // Reflexive
    bool isReflexive() {
        for (int i = 0; i < n; i++)
            if (r[i][i] != 1) return false;
        return true;
    }

    // Symmetric
    bool isSymmetric() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (r[i][j] != r[j][i]) return false;
        return true;
    }

    // Anti-Symmetric
    bool isAntiSymmetric() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (i != j && r[i][j] == 1 && r[j][i] == 1)
                    return false;
        return true;
    }

    // Transitive
    bool isTransitive() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (r[i][j])
                    for (int k = 0; k < n; k++)
                        if (r[j][k] && !r[i][k])
                            return false;
        return true;
    }

    // Check relation type
    void checkRelation() {
        bool ref = isReflexive();
        bool sym = isSymmetric();
        bool anti = isAntiSymmetric();
        bool trans = isTransitive();

        if (ref && sym && trans)
            cout << "Relation is Equivalence\n";
        else if (ref && anti && trans)
            cout << "Relation is Partial Order\n";
        else
            cout << "Relation is None\n";
    }
};

int main() {
    RELATION R;
    R.input();

    cout << "\nReflexive: " << (R.isReflexive() ? "Yes" : "No");
    cout << "\nSymmetric: " << (R.isSymmetric() ? "Yes" : "No");
    cout << "\nAnti-Symmetric: " << (R.isAntiSymmetric() ? "Yes" : "No");
    cout << "\nTransitive: " << (R.isTransitive() ? "Yes" : "No");

    cout << "\n\nResult: ";
    R.checkRelation();

    return 0;
}
# practical 3
#include <iostream>
using namespace std;

// without repetition
void permute(int a[], int l, int r) {
    if (l == r) {
        for (int i = 0; i <= r; i++) cout << a[i];
        cout << endl;
        return;
    }
    for (int i = l; i <= r; i++) {
        swap(a[l], a[i]);
        permute(a, l + 1, r);
        swap(a[l], a[i]);
    }
}

// with repetition
void repeat(int a[], int n, int r, int res[], int k) {
    if (k == r) {
        for (int i = 0; i < r; i++) cout << res[i];
        cout << endl;
        return;
    }
    for (int i = 0; i < n; i++) {
        res[k] = a[i];
        repeat(a, n, r, res, k + 1);
    }
}

int main() {
    int a[5], n, res[5];
    cout << "n: "; cin >> n;
    for (int i = 0; i < n; i++) cin >> a[i];

    cout << "\nNo Repetition:\n";
    permute(a, 0, n - 1);

    cout << "\nWith Repetition:\n";
    repeat(a, n, n, res, 0);

    return 0;
}
# practical 4
#include <iostream>
using namespace std;

int x[10], n, C;

// brute force recursion
void solve(int i, int sum) {
    if (i == n) {
        if (sum == C) {
            for (int j = 0; j < n; j++)
                cout << x[j] << " ";
            cout << endl;
        }
        return;
    }

    for (int v = 0; v <= C; v++) {
        x[i] = v;
        if (sum + v <= C)   // pruning
            solve(i + 1, sum + v);
    }
}

int main() {
    cout << "Enter n and C: ";
    cin >> n >> C;

    solve(0, 0);

    return 0;
}
# practical 5
#include <iostream>
using namespace std;

int main() {
    int n, x, result = 0;

    cout << "Enter degree of polynomial: ";
    cin >> n;

    int a[10];  // coefficients

    cout << "Enter coefficients (from highest power to constant): ";
    for (int i = 0; i <= n; i++)
        cin >> a[i];

    cout << "Enter value of x: ";
    cin >> x;

    // Evaluate polynomial
    for (int i = 0; i <= n; i++) {
        int power = 1;
        for (int j = 0; j < n - i; j++)
            power *= x;

        result += a[i] * power;
    }

    cout << "Result = " << result;

    return 0;
}
# practical 6
#include <iostream>
using namespace std;

int main() {
    int n, a[10][10];

    cout << "Enter number of vertices: ";
    cin >> n;

    cout << "Enter adjacency matrix:\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> a[i][j];

    // Check complete graph
    bool complete = true;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j && a[i][j] != 0)
                complete = false;
            if (i != j && a[i][j] != 1)
                complete = false;
        }
    }

    if (complete)
        cout << "Graph is Complete Graph";
    else
        cout << "Graph is NOT Complete Graph";

    return 0;
}
# practical 7
#include <iostream>
using namespace std;

int main() {
    int n, a[10][10];

    cout << "Enter number of vertices: ";
    cin >> n;

    cout << "Enter adjacency matrix:\n";
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> a[i][j];

    cout << "\nVertex\tIn-degree\tOut-degree\n";

    for (int i = 0; i < n; i++) {
        int indeg = 0, outdeg = 0;

        for (int j = 0; j < n; j++) {
            outdeg += a[i][j];  // row sum
            indeg += a[j][i];   // column sum
        }

        cout << i << "\t" << indeg << "\t\t" << outdeg << endl;
    }

    return 0;
}

