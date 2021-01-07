---
title:  "[알고리즘] 이분탐색(Binary Search)"
permalink: /categories/algo/binarysearch
author_profile: true
categories:
  - 자료구조와 알고리즘
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-01-05
toc: true
toc_sticky: true
---

# 개념
> 데이터가 정렬된 배열에서 가운데값을 기준으로 특정한 값을 찾아내는 탐색 알고리즘

- 이분 탐색을 하기 위해서는 반드시 데이터가 정렬된 상태여야 한다.
- **시간복잡도 O(logN)**

# 순서  
1. 배열을 오름차순으로 정렬한다.  
> {17, 28, 43, 67, 88, 92, 100}  
이 배열에서 `43`을 찾는다고 가정한다.    

2. 자료의 좌측, 우측 값을 구한다.  
`left` = 17, `right` = 100     

3. 가운데 값을 구해서 찾고하 하는 값과 비교한다.  
`mid` = (`left의 인덱스 + right의 인덱스) / 2` = (`0 + 6) / 2` = `3`  
`3`번째 배열값 = `67`  
`43` < `67`이므로 `43`은 `67`의 좌측에 존재하기 때문에 `43`의 왼쪽 부분을 탐색해주기 위해 범위를 다시 지정한다.   
`right` = `mid-1` = `3-1` = `2`  
만약, 반대로 `mid`의 배열값보다 컸다면 오른쪽을 탐색해주기 위해 다음과 같이 변경한다.   
`left` = `mid + 1`  

4. 원하는 값을 찾을때 까지 3번을 반복한다.  
> {43}  

원하는 값을 찾았다면 원소가 1개가 남았으므로 종료된다.  

# 구현
```java
int BinarySearch(int arr[], int target) {
    int left= 0;
    int right= arr.length - 1;
    int mid;

    while(left<= right) {
        mid = (left+ right) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] > target)
            right= mid - 1;
        else
            left= mid + 1;
    }
    return -1;
}
```

# 응용
## 최대값 구하기
이분탐색을 해서 데이터 범위 안에서 원하는 조건을 충족하는 최대값을 구할 수 있다.  
이때는 종료조건이 위와 다르기 때문에 항상 시뮬레이션을 해보면서 종료될 조건을 고려해주어야 한다.   
### 예시 문제
- [백준2110 공유기설치](https://www.acmicpc.net/problem/2110)
- [백준2805 나무자르기](https://www.acmicpc.net/problem/2805)

 
## 최장 증가 수열(LIS)
이분탐색을 이용해 최장 증가 수열(LIS)의 길이를 구할 수 있다.  
### 예시 문제
- [백준12015 가장 긴 증가하는 부분수열2](https://www.acmicpc.net/problem/12015)