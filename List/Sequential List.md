- 순차 리스트는 구현할 자료들을 논리적인 순서대로 메모리에 연속하여 저장하는 자료구조이다.즉, 자료의 논리적인 구조와 물리적인 구조가 일치하는 구현 방식을 갖는다.
---
```cpp
#include <iostream>

using namespace std;

int main() {
    int arr[4] = {10, 20, 30, 40}; //1차원

    for (int i = 0; i < 4; i++) {
         cout << "arr[" << i << "] = " << arr[i] << ", address : " << &arr[i] << endl;
    }

    int arr2[2][3] = { {50, 30, 10}, {12, 27, 51} }; //2 차원

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            cout << "arr[" << i << "][" << j << "] = " << arr2[i][j] << ", address : " << &arr2[i][j] << endl;
        }
    }

    return 0;
    
}
```

## 정리
- 요약하면, 순차 리스트(Sequential List)는 구현할 자료들을 논리적인 순서대로 메모리에 연속하여 저장하는 자료구조이다.
- 삽입과 삭제 연산에는 비효율적이지만, 탐색에는 효율적이다.
