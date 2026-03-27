# discrete-maths
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
