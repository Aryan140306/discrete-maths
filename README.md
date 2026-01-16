# discrete-maths
class SET:
    def __init__(self):
        self.myset = set(map(int, input("Enter values of set (space separated): ").split()))

    # user-defined member function
    def is_member(self):
        element=int(input('enter the no. you want to search:'))

        if element in self.myset:
            print('True')
        else:
            print('False')


    def power_set(self):
        n = len(self.myset)
        print("Power Set:")

        for i in range(1 << n):   # 2^n subsets
            subset = []
            for j in range(n):
                if i & (1 << j):
                    subset.append(self.myset[j])
            print(subset)
            

s=SET()
s.is_member()
s.power_set()
