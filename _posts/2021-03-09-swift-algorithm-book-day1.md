---
comments: true
title: Swift ) 순환 버퍼, 
key: 202103091
modify_date: 2021-03-09
picture_frame: shadow
tags:
  - [Algorithm]
  - [데이터 구조]
---
 
## 순환 버퍼(Ring Buffer)
 
순환 버퍼는 **고정 크기의 데이터 구조**로, Ring의 구조와 비슷하다.   
만약 버퍼가 데이터로 꽉 차면 버퍼의 시작 부분을 뜻하는 헤드 인덱스가 0으로 되돌아 가며, 기존 데이터 중 가장 먼저 저장된 데이터가 밀려나고 새로운 데이터가 저장된다.   
 
이러한 특징으로 인해 순환 버퍼는 특히 **FIFO** 데이터 구조를 구현할 때 유용하다.   
큐 데이터 구조 역시 FIFO와 같은 형식이지만 순환 버퍼는 **헤드 인덱스와 테일 인덱스가 맞물려 있다는 점**에서 다르다.
 
```
public struct RingBuffer<T> { 
    private var array: [T?]
    private var readIndex = 0 
    private var writeIndex = 0 
    
    public init(count: Int) {
        array = Array<T?>(repeating: nil, count: count)
    }
    
    public var first: T? {
        array[readIndex]
    } 
    
    public mutating func write(_ element: T) -> Bool { 
        if !isFull {
            array[writeIndex % array.count] = element 
            writeIndex += 1
            return true
        } else {
            return false 
        }
    }
    
    public mutating func read() -> T? { 
        if !isEmpty {
            let element = array[readIndex % array.count]
            readIndex += 1 
            return element 
        } else {
            return nil 
        }
    }
    
    private var availableSpaceForReading: Int {
        writeIndex - readIndex 
    }
    
    public var isEmpty: Bool {
        availableSpaceForReading == 0
    }
    
    private var availableSpaceForWriting: Int {
        array.count - availableSpaceForReading 
    }
    
    public var isFull: Bool {
        availableSpaceForWriting == 0
    }
}
```
여기까지는 떠뜸떠뜸 이해했는데, 이 다음부터 다시 이해 안되기 시작..
```
extension RingBuffer: CustomStringConvertible { 
    public var description: String {
        let values = (0..<availableSpaceForReading).map {
            String(describing: array[($0 + readIndex) % array.count]!)
        }
        return "[" + values.joined(separator: ", ") + "]"
    }
}
```

 
### 장점
 
- 배열 데이터 구조보다 데이터 저장에 효율적이다.
- 버퍼의 메모리 크기가 안정적인 상태를 유지한다.
- 구현할 때, 버퍼의 크기를 조절하고 기존의 데이터를 새로 생성된 버퍼로 전달하는 기능이 추가된다.

#### Reference)
 
[https://iospanda.tistory.com/entry/Swift-Queue-Ring-Buffer-Double-Stack%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-Queue-%EA%B5%AC%ED%98%84%EA%B3%BC-%EA%B7%B8-%EC%98%88](https://iospanda.tistory.com/entry/Swift-Queue-Ring-Buffer-Double-Stack%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-Queue-%EA%B5%AC%ED%98%84%EA%B3%BC-%EA%B7%B8-%EC%98%88)
